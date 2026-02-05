<h2>Providers in Terraform</h2>

<p>
A provider in Terraform is a plugin that enables Terraform to interact with an API.
This includes cloud providers, SaaS providers, and other infrastructure or service APIs.
Providers tell Terraform <strong>which services to talk to</strong> and
<strong>how to manage resources</strong>.
</p>

<p>
Providers are defined in Terraform configuration files and are required for creating,
updating, and destroying infrastructure resources.
</p>

<hr>

<h3>Example: AWS Provider</h3>

<p>
To create a virtual machine on AWS using Terraform, you must configure the
<strong>aws</strong> provider. The AWS provider exposes resources such as EC2 instances,
VPCs, S3 buckets, and more.
</p>

<pre><code>provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  ami           = "ami-0123456789abcdef0"  # Change the AMI
  instance_type = "t2.micro"
}
</code></pre>

<p>
In this example:
</p>
<ul>
  <li>The <code>aws</code> provider is configured with the <code>us-east-1</code> region</li>
  <li>An EC2 instance is created using the <code>aws_instance</code> resource</li>
</ul>

<p>
When Terraform runs:
</p>
<ol>
  <li>Terraform downloads and installs the AWS provider</li>
  <li>The provider communicates with AWS APIs</li>
  <li>The EC2 instance is created based on the configuration</li>
</ol>

<hr>

<h3>Other Common Terraform Providers</h3>

<ul>
  <li><strong>azurerm</strong> – Microsoft Azure</li>
  <li><strong>google</strong> – Google Cloud Platform</li>
  <li><strong>kubernetes</strong> – Kubernetes clusters</li>
  <li><strong>openstack</strong> – OpenStack</li>
  <li><strong>vsphere</strong> – VMware vSphere</li>
</ul>

<p>
Terraform supports hundreds of providers, and new providers are continuously added by
HashiCorp and the community.
</p>

<hr>

<h2>Ways to Configure Providers in Terraform</h2>

<p>
There are three main ways to configure providers in Terraform. The best approach depends
on project complexity and reuse requirements.
</p>

<h3>1. Configure Provider in the Root Module</h3>

<p>
This is the most common and simplest approach. The provider configuration is defined
in the root module and is available to all resources.
</p>

<pre><code>provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  ami           = "ami-0123456789abcdef0"
  instance_type = "t2.micro"
}
</code></pre>

<p>
<strong>Use this approach when:</strong>
</p>
<ul>
  <li>You are using a single provider</li>
  <li>Your infrastructure is simple</li>
</ul>

<hr>

<h3>2. Configure Provider in a Child Module</h3>

<p>
Providers can be passed explicitly to child modules. This is useful when working with
multiple regions or multiple provider configurations.
</p>

<pre><code>module "aws_vpc" {
  source = "./aws_vpc"

  providers = {
    aws = aws.us-west-2
  }
}

resource "aws_instance" "example" {
  ami           = "ami-0123456789abcdef0"
  instance_type = "t2.micro"

  depends_on = [module.aws_vpc]
}
</code></pre>

<p>
<strong>Use this approach when:</strong>
</p>
<ul>
  <li>You reuse modules across environments</li>
  <li>You need different provider configurations (regions, accounts)</li>
</ul>

<hr>

<h3>3. Configure Providers Using <code>required_providers</code></h3>

<p>
The <code>required_providers</code> block ensures a specific provider and version is used.
This is considered a best practice for production environments.
</p>

<pre><code>terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 3.79"
    }
  }
}

resource "aws_instance" "example" {
  ami           = "ami-0123456789abcdef0"
  instance_type = "t2.micro"
}
</code></pre>

<p>
<strong>Use this approach when:</strong>
</p>
<ul>
  <li>You want version consistency across teams</li>
  <li>You are working in collaborative or CI/CD environments</li>
</ul>

<hr>

<h3>Choosing the Right Provider Configuration</h3>

<ul>
  <li>
    <strong>Single provider, simple setup:</strong> Root module configuration
  </li>
  <li>
    <strong>Multiple regions or reusable modules:</strong> Child module configuration
  </li>
  <li>
    <strong>Production-grade stability:</strong> <code>required_providers</code>
  </li>
</ul>

<p>
Providers are a core component of Terraform. They enable Terraform to manage infrastructure
across cloud platforms, services, and APIs, making Terraform a powerful and flexible
Infrastructure as Code tool.
</p>
