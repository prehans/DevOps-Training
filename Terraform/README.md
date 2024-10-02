Terraform is an open-source infrastructure as code (IaC) tool developed by HashiCorp. It allows users to define and provision data center infrastructure using a high-level configuration language called HashiCorp Configuration Language (HCL) or JSON.

### Key Features:

1. **Infrastructure as Code**: Infrastructure is defined in code, allowing versioning, reusability, and automation.
2. **Provider Support**: Terraform supports a wide range of cloud providers (AWS, Azure, GCP, etc.) and on-premise services (VMware, OpenStack, etc.).
3. **Declarative Language**: You specify _what_ infrastructure you want, and Terraform figures out _how_ to achieve it.
4. **State Management**: Terraform keeps track of resources and their current state using a state file. This allows it to track changes and apply only the necessary modifications.
5. **Modules**: Reusable blocks of Terraform configuration, enabling users to manage infrastructure components more easily.

### Basic Workflow:

1. **Write**: Create configuration files that describe the desired infrastructure.
2. **Plan**: Terraform analyzes the infrastructure plan to show the proposed changes.
3. **Apply**: Terraform provisions and manages the infrastructure.
4. **Destroy**: Tear down the infrastructure when it's no longer needed.

### Use Cases:

- Provisioning cloud resources (VMs, databases, networking, etc.).
- Managing complex infrastructure across multiple environments.
- Automating the deployment and scaling of applications.

### Example:

Here’s a simple example of a Terraform configuration for deploying an AWS EC2 instance:

```hcl
provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
```

In this example, Terraform is configured to create an EC2 instance using the specified AMI and instance type in the AWS region "us-west-2".

Terraform is widely used for managing cloud infrastructure in a repeatable and scalable way, making it popular in DevOps environments for automating infrastructure deployment.

- **`terraform init`**: Prepare local environment for setting up the cloud infrastructure.
- **`terraform plan`**: It tells how many resources you are going to add update of delete.
- **`terraform apply`**: Run the virtual instances on cloud platforms.
- **`terraform destroy`**: Destroys all infrastructure managed by the Terraform configuration, instances or resources.

In Terraform, the `variable.tf` file is used to define variables that can be reused across your configuration files. This allows you to parameterize your Terraform configurations, making them more dynamic and flexible. Here's an example of how you can define variables for the region, instance count, and instance type in a `variables.tf` file:

# Terraform variables

https://jhooq.com/terraform-input-variables/

### `variables.tf`

```hcl
# Define the AWS region as a variable
variable "aws_region" {
  description = "The AWS region where resources will be created"
  type        = string
  default     = "us-west-2"
}

# Define the instance type as a variable
variable "instance_type" {
  description = "The type of instance to create"
  type        = string
  default     = "t2.micro"
}

# Define the number of instances to create as a variable
variable "instance_count" {
  description = "The number of EC2 instances to create"
  type        = number
  default     = 3
}

# Define the AMI ID as a variable
variable "ami_id" {
  description = "The AMI ID for the EC2 instance"
  type        = string
  default     = "ami-0c55b159cbfafe1f0"  # Replace with your AMI ID
}
```

### `main.tf` (updated to use variables)

```hcl
# Use the AWS provider with the region from the variable
provider "aws" {
  region = var.aws_region
}

# Create a security group allowing SSH and HTTP traffic
resource "aws_security_group" "web_sg" {
  name        = "web_sg"
  description = "Allow SSH and HTTP traffic"

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]  # Allow SSH from anywhere (use with caution)
  }

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]  # Allow HTTP from anywhere
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"  # Allow all outbound traffic
    cidr_blocks = ["0.0.0.0/0"]
  }
}

# Create multiple EC2 instances using the instance_count variable
resource "aws_instance" "my_instance" {
  count         = var.instance_count   # Number of instances based on variable
  ami           = var.ami_id           # AMI ID from variable
  instance_type = var.instance_type    # Instance type from variable
  security_groups = [aws_security_group.web_sg.name]

  tags = {
    Name = "My_Terraform_EC2_${count.index}"  # Unique name for each instance
  }
}
```

### Key Points:

- **Variables**: Defined in `variables.tf`, these can be reused in other configuration files like `main.tf`.
- **Defaults**: Each variable has a default value, but you can override these values by passing them via a `terraform.tfvars` file or command line during execution.
- **Flexibility**: This makes the configuration more flexible and customizable without changing the core code.

### Steps to use:

1. **Initialize Terraform**:

   ```bash
   terraform init
   ```

2. **Plan the deployment**:

   ```bash
   terraform plan
   ```

3. **Apply the configuration**:
   ```bash
   terraform apply
   ```

With this setup, you can easily change parameters (like region, instance type, or number of instances) without modifying the core logic of your Terraform configuration.

https://jhooq.com/terraform-variable-and-tfvars-file/

# Terraform Locals

https://jhooq.com/how-to-use-terraform-locals/

In Terraform, **locals** are used to assign local values to simplify complex expressions or avoid repeating the same value multiple times within a module. These local values are scoped to the module in which they are defined, meaning they are not exposed outside the module and cannot be passed as inputs.

### Syntax:

Local values are defined inside a `locals` block and referenced with the `local.<variable_name>` syntax.

### Example of Terraform `locals`:

#### `main.tf`

```hcl
provider "aws" {
  region = "us-west-2"
}

# Define local values
locals {
  environment       = "production"
  instance_type     = "t2.micro"
  instance_count    = 3
  app_name          = "MyApp"
  full_instance_name = "${local.app_name}-${local.environment}"
}

# Create multiple EC2 instances using locals
resource "aws_instance" "my_instance" {
  count         = local.instance_count        # Use local value for count
  ami           = "ami-0c55b159cbfafe1f0"     # Replace with appropriate AMI
  instance_type = local.instance_type         # Use local value for instance type
  security_groups = [aws_security_group.web_sg.name]

  tags = {
    Name = "${local.full_instance_name}-${count.index}"  # Use local value for name
  }
}
```

### Key Points:

- **`locals` block**: This is where you define the local values. In this example, variables like `environment`, `instance_type`, `app_name`, and `full_instance_name` are declared.
- **Referencing**: You reference a local variable using `local.<variable_name>`. For example, `local.instance_type` or `local.full_instance_name`.
- **Reusability**: Local values are useful to store computed values or values that are reused multiple times in the same module.

### Example Breakdown:

- **`local.environment`**: Stores the environment name (`production`).
- **`local.full_instance_name`**: Concatenates the application name (`MyApp`) and the environment name (`production`), resulting in `MyApp-production`.
- **`local.instance_count`**: Specifies that 3 instances should be created.

### Benefits of Locals:

1. **Simplify Code**: Instead of repeating the same values across your Terraform files, you can define them once and reuse them.
2. **Improve Readability**: Local variables make the code more readable by breaking down complex expressions into simpler parts.
3. **Avoid Duplication**: Prevents hardcoding the same value in multiple places, making the configuration easier to maintain and modify.

### When to Use Locals:

- When you need to reuse the same values across multiple resources.
- When you have complex expressions that can be simplified.
- When you need computed values (e.g., concatenating strings or performing calculations).

Locals are an excellent way to streamline your Terraform configurations without making your code dependent on external inputs or exposing values externally.

# Terraform Output

https://jhooq.com/how-to-use-terraform-output-values/

# Terraform loops

https://jhooq.com/terraform-for-and-for-each-loop/

# Terraform Provisioners

https://jhooq.com/terraform-provisioner/

# Terraform Dynamic Block

https://jhooq.com/terraform-dynamic-block/

# Terraform Module

(again go through)

https://jhooq.com/terraform-module/

# Terraform Workspaces

https://jhooq.com/terraform-workspaces/

In Terraform, **workspaces** are a way to manage multiple environments (like `dev`, `qa`, `prod`) within the same configuration. Each workspace can have its own state and resources, allowing you to manage isolated environments using a single set of Terraform code.

### Key Features of Workspaces:

- **Multiple Environments**: Workspaces help you manage different environments (e.g., dev, qa, prod) with the same configuration.
- **Separate States**: Each workspace maintains its own state file, ensuring that resources created in one workspace do not interfere with those in another.
- **Easy Switching**: You can easily switch between workspaces using Terraform commands.

### Workspace Commands:

1. **Create a New Workspace**

   ```bash
   terraform workspace new <workspace_name>
   ```

   - This command creates a new workspace with the specified name.
   - Example:
     ```bash
     terraform workspace new dev
     ```

2. **List All Workspaces**

   ```bash
   terraform workspace list
   ```

   - Lists all available workspaces in the current configuration.
   - Example output:
     ```bash
     default
     * dev
     qa
     prod
     ```

3. **Show the Current Workspace**

   ```bash
   terraform workspace show
   ```

   - Displays the name of the current workspace.
   - Example:
     ```bash
     dev
     ```

4. **Switch to a Workspace**

   ```bash
   terraform workspace select <workspace_name>
   ```

   - Switches to the specified workspace.
   - Example:
     ```bash
     terraform workspace select prod
     ```

5. **Delete a Workspace**
   ```bash
   terraform workspace delete <workspace_name>
   ```
   - Deletes a specified workspace. Note that you cannot delete the workspace you are currently in.
   - Example:
     ```bash
     terraform workspace delete qa
     ```

### Example Usage of Workspaces:

Suppose you are working with different environments (`dev`, `qa`, `prod`). Instead of creating separate Terraform files for each environment, you can use workspaces to manage them within the same configuration.

1. **Define Resources in `main.tf`:**

   ```hcl
   provider "aws" {
     region = "us-west-2"
   }

   resource "aws_instance" "my_instance" {
     count         = var.instance_count
     ami           = "ami-0c55b159cbfafe1f0"  # Replace with valid AMI ID
     instance_type = "t2.micro"

     tags = {
       Name = "${terraform.workspace}-instance"
     }
   }

   variable "instance_count" {
     default = 1
   }
   ```

2. **Switch to `dev` Workspace:**

   ```bash
   terraform workspace new dev
   ```

3. **Run Terraform Commands for `dev`:**

   ```bash
   terraform plan
   terraform apply
   ```

4. **Switch to `prod` Workspace:**

   ```bash
   terraform workspace select prod
   ```

5. **Run Terraform Commands for `prod`:**
   ```bash
   terraform plan
   terraform apply
   ```

### Benefits of Using Workspaces:

- **Isolated State**: Workspaces maintain separate state files for each environment, ensuring that changes in one environment do not affect another.
- **Code Reusability**: You can use the same Terraform configuration to manage multiple environments, avoiding duplication of code.
- **Environment-Specific Configurations**: You can dynamically adjust configurations based on the current workspace using `terraform.workspace`, enabling environment-specific settings.

### Workspace Considerations:

- **Not for Every Use Case**: Workspaces are useful for isolated environments like `dev`, `qa`, and `prod`, but they might not be ideal for large-scale infrastructure management with complex branching.
- **Workspaces are Local to the Directory**: Workspaces are specific to the working directory of your Terraform configuration.

### Example of Using `terraform.workspace` in Variables:

You can use `terraform.workspace` to adjust behavior based on the current workspace:

```hcl
variable "instance_count" {
  default = {
    default = 1
    dev     = 1
    prod    = 3
  }
}

resource "aws_instance" "my_instance" {
  count         = var.instance_count[terraform.workspace]
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  tags = {
    Name = "${terraform.workspace}-instance"
  }
}
```

This example uses `terraform.workspace` to adjust the number of instances based on the current workspace (`dev` or `prod`).
