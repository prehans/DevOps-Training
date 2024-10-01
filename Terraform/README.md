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
