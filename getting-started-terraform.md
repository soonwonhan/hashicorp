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

## Installing Terraform

To install Terraform, 
1. Visit [Terraform.io](https://developer.hashicorp.com/terraform/downloads).
2. Select the operating system for your device.
3. Download the latest version of Terraform.

Let's start by creating some infrastructure.

## Creating Infrastructure

1. Open your Command-Line Interface.
2. Create a new directory on your local machine.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

3. Next, create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

4. Paste the following lines into the file.

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

## Applying provisions

1. Initialize Terraform with the `init` command. The AWS provider will be installed. 

```shell
$ terraform init
```

2. Check for any errors. If it ran successfully, provision the resource with the `apply` command.

```shell
$ terraform apply
```

3. The command will take up to a few minutes to run and will display a message once the resource is created.


## Destroying Infrastructure

1. Finally, destroy the infrastructure.

```shell
$ terraform destroy
```

2. Look for a message at the bottom of the output asking for confirmation. Type `yes` and hit ENTER. Terraform will destroy the resources it had created earlier.


# Next Steps
You have successfully completed your first Terraform tutorial. You installed Terraform, applied your first file to AWS, and destroyed an infrastructure.
You can now move on to exploring more in-depth Terraform tutorials here: [Tutorials](https://developer.hashicorp.com/terraform/tutorials)

## Additional Resources
* [Documentation](https://developer.hashicorp.com/terraform/docs)
* [Tutorials](https://developer.hashicorp.com/terraform/tutorials)
* [Webinars](https://www.hashicorp.com/events/webinars/recorded?product=terraform&type=all)
* [Blogs](https://www.hashicorp.com/blog/products/terraform)
