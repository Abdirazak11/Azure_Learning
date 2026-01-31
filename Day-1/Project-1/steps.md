<h2>Terraform Project Setup (AWS Example)</h2>

<h3>Create a Terraform Project Directory</h3>
<p>
Create a directory for your Terraform project and add a Terraform configuration file
(usually named <code>main.tf</code>). This file defines the AWS provider and the resources
you want to create.
</p>

<h3>Example Terraform Configuration</h3>

<pre><code>provider "aws" {
  region = "us-east-1"  # Set your desired AWS region
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"  # Specify an appropriate AMI ID
  instance_type = "t2.micro"
}
</code></pre>

<h3>Initialize Terraform</h3>
<p>
Navigate to the directory containing your Terraform configuration files and run:
</p>

<pre><code>terraform init
</code></pre>

<p>
This command initializes the Terraform working directory and downloads the required
provider plugins.
</p>

<h3>Apply the Configuration</h3>
<p>
Run the following command to create the AWS resources defined in your configuration:
</p>

<pre><code>terraform apply
</code></pre>

<p>
Terraform will display an execution plan showing the changes it will make.
Review the plan carefully and type <strong>yes</strong> when prompted.
</p>

<h3>Verify Resources</h3>
<p>
After Terraform completes provisioning, verify the created resources using:
</p>
<ul>
  <li>The AWS Management Console</li>
  <li>AWS CLI commands (e.g., <code>aws ec2 describe-instances</code>)</li>
</ul>

<h3>Destroy Resources</h3>
<p>
To remove all resources created by Terraform, run:
</p>

<pre><code>terraform destroy
</code></pre>

<p>
<strong>⚠️ Warning:</strong> Use this command carefully, as it permanently deletes
resources defined in your Terraform configuration.
</p>
