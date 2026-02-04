<h2>Multiple Providers in Terraform</h2>

<p>
Terraform allows you to use <strong>multiple providers</strong> within a single project.
This makes it possible to provision and manage infrastructure across different cloud
platforms such as AWS, Azure, Google Cloud, and more—using a single Terraform workflow.
</p>

<p>
Using multiple providers is common in:
</p>
<ul>
  <li>Multi-cloud architectures</li>
  <li>Hybrid cloud environments</li>
  <li>Migration scenarios between cloud providers</li>
</ul>

<hr>

<h3>Defining Multiple Providers</h3>

<p>
A recommended best practice is to define provider configurations in a dedicated
<code>providers.tf</code> file located in the root directory of your Terraform project.
</p>

<p>
Below is an example defining both AWS and Azure providers:
</p>

<pre><code>provider "aws" {
  region = "us-east-1"
}

provider "azurerm" {
  subscription_id = "your-azure-subscription-id"
  client_id       = "your-azure-client-id"
  client_secret   = "your-azure-client-secret"
  tenant_id       = "your-azure-tenant-id"
}
</code></pre>

<p>
Each provider block contains authentication and configuration details specific to the
cloud platform it manages.
</p>

<hr>

<h3>Using Multiple Providers in Resources</h3>

<p>
Once the providers are defined, you can reference them directly in your Terraform
configuration files to create resources in different cloud environments.
</p>

<h4>AWS Resource Example</h4>

<pre><code>resource "aws_instance" "example" {
  ami           = "ami-0123456789abcdef0"
  instance_type = "t2.micro"
}
</code></pre>

<h4>Azure Resource Example</h4>

<pre><code>resource "azurerm_virtual_machine" "example" {
  name     = "example-vm"
  location = "eastus"
  size     = "Standard_A1"
}
</code></pre>

<p>
In this setup:
</p>
<ul>
  <li>The <code>aws_instance</code> resource is created in AWS</li>
  <li>The <code>azurerm_virtual_machine</code> resource is created in Azure</li>
</ul>

<hr>

<h3>Benefits of Using Multiple Providers</h3>

<ul>
  <li>Centralized infrastructure management across clouds</li>
  <li>Consistent provisioning workflow</li>
  <li>Easier migration between cloud platforms</li>
  <li>Improved flexibility and vendor independence</li>
</ul>

<hr>

<h3>Best Practices</h3>

<ul>
  <li>Store provider credentials securely using environment variables or secret managers</li>
  <li>Use <code>required_providers</code> to pin provider versions</li>
  <li>Separate provider configuration into <code>providers.tf</code> for clarity</li>
  <li>Use provider aliases when managing multiple accounts or regions</li>
</ul>

<p>
Using multiple providers is one of Terraform’s strongest features and enables true
multi-cloud and hybrid-cloud Infrastructure as Code implementations.
</p>
