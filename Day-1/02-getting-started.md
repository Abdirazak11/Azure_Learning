<h2>Getting Started with Terraform</h2>

<p>
To get started with Terraform, it’s important to understand some key terminology and
core concepts. These fundamentals form the foundation of how Terraform works and
how Infrastructure as Code (IaC) is implemented.
</p>

<h3>Core Terraform Concepts</h3>

<h4>Provider</h4>
<p>
A provider is a plugin that allows Terraform to interact with a specific cloud or
infrastructure platform. Providers define how resources are created and managed.
</p>
<p>
<strong>Examples:</strong> AWS, Azure, Google Cloud, Kubernetes
</p>

<h4>Resource</h4>
<p>
A resource represents an infrastructure component managed by Terraform. Resources
can include virtual machines, databases, storage buckets, networking components,
and more.
</p>

<h4>Module</h4>
<p>
A module is a reusable and self-contained collection of Terraform configuration files.
Modules help organize infrastructure code, improve reusability, and simplify maintenance.
</p>
<p>
Modules can be custom-built or sourced from the Terraform Registry.
</p>

<h4>Configuration File</h4>
<p>
Terraform configuration files (with a <code>.tf</code> extension) define the desired
state of your infrastructure. These files specify providers, resources, variables,
outputs, and backend configurations.
</p>
<p>
The primary file is commonly named <code>main.tf</code>, though multiple files can be
used in a project.
</p>

<h4>Variable</h4>
<p>
Variables act as placeholders for values in Terraform configurations. They make
infrastructure code flexible and reusable by allowing values to be passed dynamically.
</p>

<h4>Output</h4>
<p>
Outputs are values produced after Terraform applies a configuration. They are often
used to display important information such as IP addresses, resource IDs, or to pass
values to other systems.
</p>

<h4>State File</h4>
<p>
Terraform maintains a state file (typically <code>terraform.tfstate</code>) that tracks
the real-world state of infrastructure. The state file allows Terraform to determine
what changes are required when configurations are updated.
</p>

<h4>Plan</h4>
<p>
A plan is a preview of the actions Terraform will take to reach the desired state.
Running <code>terraform plan</code> shows what resources will be created, modified,
or destroyed before applying changes.
</p>

<h4>Apply</h4>
<p>
The <code>terraform apply</code> command executes the actions described in the plan.
It provisions, updates, or deletes infrastructure resources as defined in the
Terraform configuration.
</p>

<h4>Workspace</h4>
<p>
Workspaces allow you to manage multiple environments such as development, staging,
and production using the same Terraform configuration but separate state files.
</p>

<h4>Remote Backend</h4>
<p>
A remote backend stores Terraform state files outside the local system. This improves
collaboration, security, and reliability.
</p>
<p>
<strong>Common remote backends:</strong> Amazon S3, Azure Blob Storage, Terraform Cloud
</p>

<p>
These concepts form the backbone of Terraform workflows. As you gain hands-on experience,
you’ll see how they work together to enable scalable, reliable, and automated
infrastructure management.
</p>
