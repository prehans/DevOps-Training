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
