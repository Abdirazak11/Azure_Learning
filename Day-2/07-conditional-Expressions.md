<h2>Conditional Expressions in Terraform</h2>

<p>
Conditional expressions in Terraform allow you to apply <strong>decision-making logic</strong>
within your infrastructure code. They help control resource creation, configuration values,
and behavior based on conditions.
</p>

<p>
Conditional expressions are commonly used to:
</p>
<ul>
  <li>Enable or disable resource creation</li>
  <li>Change configuration values based on environment</li>
  <li>Control access rules and feature toggles</li>
</ul>

<hr>

<h3>Syntax of Conditional Expressions</h3>

<pre><code>condition ? true_value : false_value
</code></pre>

<ul>
  <li><strong>condition</strong> – An expression that evaluates to <code>true</code> or <code>false</code></li>
  <li><strong>true_value</strong> – Returned when the condition is true</li>
  <li><strong>false_value</strong> – Returned when the condition is false</li>
</ul>

<hr>

<h3>Conditional Resource Creation</h3>

<p>
Conditional expressions are often used with the <code>count</code> meta-argument to control
whether a resource is created.
</p>

<pre><code>resource "aws_instance" "example" {
  count = var.create_instance ? 1 : 0

  ami           = "ami-XXXXXXXXXXXXXXXXX"
  instance_type = "t2.micro"
}
</code></pre>

<p>
If <code>var.create_instance</code> is:
</p>
<ul>
  <li><strong>true</strong> → One EC2 instance is created</li>
  <li><strong>false</strong> → No EC2 instances are created</li>
</ul>

<hr>

<h3>Conditional Variable-Based Configuration</h3>

<p>
Conditional expressions can dynamically assign values based on environment or other variables.
</p>

<h4>Variable Definitions</h4>

<pre><code>variable "environment" {
  description = "Environment type"
  type        = string
  default     = "development"
}

variable "production_subnet_cidr" {
  description = "CIDR block for production subnet"
  type        = string
  default     = "10.0.1.0/24"
}

variable "development_subnet_cidr" {
  description = "CIDR block for development subnet"
  type        = string
  default     = "10.0.2.0/24"
}
</code></pre>

<h4>Conditional Usage in a Resource</h4>

<pre><code>resource "aws_security_group" "example" {
  name        = "example-sg"
  description = "Example security group"

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = var.environment == "production"
      ? [var.production_subnet_cidr]
      : [var.development_subnet_cidr]
  }
}
</code></pre>

<p>
This configuration applies different CIDR blocks depending on whether the environment
is production or development.
</p>

<hr>

<h3>Conditional Resource Configuration</h3>

<p>
Conditional expressions can also control specific resource attributes.
</p>

<pre><code>resource "aws_security_group" "example" {
  name        = "example-sg"
  description = "Example security group"

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = var.enable_ssh ? ["0.0.0.0/0"] : []
  }
}
</code></pre>

<p>
If <code>enable_ssh</code> is:
</p>
<ul>
  <li><strong>true</strong> → SSH access is allowed from anywhere</li>
  <li><strong>false</strong> → No SSH ingress rule is applied</li>
</ul>

<hr>

<h3>Best Practices</h3>

<ul>
  <li>Use conditional expressions to avoid duplicated code</li>
  <li>Prefer <code>count</code> or <code>for_each</code> for conditional resource creation</li>
  <li>Keep conditions simple and readable</li>
  <li>Use variables and locals to centralize logic</li>
</ul>

<hr>

<h3>Conclusion</h3>

<p>
Conditional expressions are a powerful Terraform feature that enable dynamic,
environment-aware, and reusable infrastructure definitions. When used correctly,
they significantly improve flexibility and maintainability of IaC code.
</p>
