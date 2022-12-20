# Getting Started with Terraform

Terraform is the most popular langauge for defining and provisioning infrastructure as code (IaC). 
Through this tutorial, you will learn how to:
* Install Terraform
* Create a file for your Terraform configuration code
* Apply planned provisions to your infrastructure
* Destroy a preexisting infrastructure

## Prerequisites
* Command-Line Interface
  - Mac terminal, Windows Command Prompt
* Infrastructure provider
  - Amazon Web Services, Azure, Terraform Cloud, Google Cloud Platform, Oracle Cloud, Docker

To install Terraform, 
1. Simply visit [Terraform.io](https://developer.hashicorp.com/terraform/downloads).
2. Select the operating system for your device.
3. Download the latest version of Terraform.
4. Open the download and follow the installation steps.

Let's start creating some infrastructure.

Most guys find it easiest to create a new directory on their local machine through the terminal. 

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

Next, create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

Paste the following lines into the file.

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}
provider "docker" {
    host = "unix:///var/run/docker.sock"
}
resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}
resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

Initialize Terraform with the `init` command. The AWS provider will be installed. 

```shell
$ terraform init
```

Check for any errors. If it ran successfully, provision the resource with the `apply` command.

```shell
$ terraform apply
```

The command will take up to a few minutes to run and will display a message once the resource is created.

Finally, destroy the infrastructure.

```shell
$ terraform destroy
```

Look for a message at the bottom of the output asking for confirmation. Type `yes` and hit ENTER. Terraform will destroy the resources it had created earlier.
