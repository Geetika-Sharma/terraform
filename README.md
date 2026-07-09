# Complete Terraform Course - From BEGINNER to PRO! (Learn Infrastructure as Code) Notes

[Video Link](https://www.youtube.com/watch?v=7xngnjfIlK4)

## Part 1
### Provisioning Cloud Resources
- GUI
- API/CLI
- IaC
  - **Ad-hoc Scripts** e.g Bash Script, PowerShell
  - **Configuration Management Tools** e.g. Ansible, Puppet
  - **Server Templating Tools** - e.g VM Image, Base Image
  - **Orchestration Tools** - e.g Kubernetes, OpenShift
  - **Provisioning Tools** - e.g Terraform, Pulumi, AWS CloudFormation, Azure Resource Manager
    - **Declarative**: You define the *desired end state*, and the system figures out how to achieve it - e.g., using **Terraform** to declare “I want 3 EC2 instances,” and it provisions them automatically.
    - **Imperative**: You define the *exact steps to execute* to reach the result — e.g., writing a Bash script that runs commands one by one to create 3 EC2 instances manually.

### IaC Provisioning Tool Landscape
<img width="728" height="294" alt="image" src="https://github.com/user-attachments/assets/4378810f-d98f-400e-8c9b-6f6f60d8f28a" />

## Part 2

### What is Terraform
* **Terraform** is an open-source Infrastructure as Code (IaC) tool used to **provision and manage cloud and on-prem infrastructure** using code.

* It uses a **declarative configuration language (HCL)** where you define the desired state, and Terraform creates and updates resources to match it.

* It is **cloud-agnostic**, meaning it can manage infrastructure across AWS, Azure, GCP, Kubernetes, and many other platforms using providers.

### Terraform Architecture
<img width="1510" height="756" alt="image" src="https://github.com/user-attachments/assets/cfc4f77a-0067-430d-b6c4-266b542cbf49" />


### Common Patterns

#### 🔹 Provisioning + Configuration Management
**Example:** Use **Terraform** to provision an EC2 instance on AWS, then use **Ansible** to install and configure Nginx on that server.

#### 🔹 Provisioning + Server Templating
**Example:** Use **Packer** to create a custom machine image with pre-installed software, then use **Terraform** to provision infrastructure using that image.

#### 🔹 Provisioning + Orchestration 
**Example:** Use **Terraform** to provision a Kubernetes cluster (e.g., EKS/AKS/GKE), then use **Kubernetes** to deploy and manage containerized applications within that cluster.

## Part 3
### Basic Usage Command
<img width="536" height="460" alt="image" src="https://github.com/user-attachments/assets/f4b78c52-359d-4bb4-8d6c-2a3c8c5a6d3b" />

#### terraform init
The terraform init command initializes a working directory containing Terraform configuration files. This is the first command you should run after writing a new Terraform configuration or cloning an existing configuration from version control. It is safe to run this command multiple times.

<img width="1012" height="481" alt="image" src="https://github.com/user-attachments/assets/ef4229c7-f33d-4804-bbf9-15c7fcb4e9e2" />
<img width="1388" height="731" alt="image" src="https://github.com/user-attachments/assets/44cb078e-aa39-4eed-9b61-f3e22717b3b2" />

#### terraform plan
The terraform plan command creates an execution plan, which lets you preview the changes that Terraform plans to make to your infrastructure.
By default, Terraform performs the following operations when it creates a plan:

- Reads the current state of any already-existing remote objects to make sure that the Terraform state is up-to-date.
- Compares the current configuration to the prior state and noting any differences.
- Proposes a set of change actions that should, if applied, make the remote objects match the configuration.

<img width="1490" height="638" alt="image" src="https://github.com/user-attachments/assets/9fad0ef1-1acd-4aa5-803d-f0229cda8c74" />

#### terraform apply
The terraform apply command executes the operations proposed in a Terraform plan.
<img width="1027" height="564" alt="image" src="https://github.com/user-attachments/assets/4d11e485-2e32-4350-b2ae-755a0ed6a34d" />

#### terraform destroy
The terraform destroy command deprovisions all objects managed by a Terraform configuration.

While you will typically not want to destroy long-lived objects in a production environment, Terraform is sometimes used to manage ephemeral infrastructure for development purposes, in which case you can use terraform destroy to conveniently clean up all of those temporary objects once you are finished with your work.

<img width="1459" height="778" alt="image" src="https://github.com/user-attachments/assets/b7057fce-efb1-4aa3-9ef4-03251796195a" />

### State File
<img width="1472" height="779" alt="image" src="https://github.com/user-attachments/assets/a1c75fd1-e4d7-42f8-a707-302c8064a53e" />

#### Local Backend
<img width="905" height="510" alt="image" src="https://github.com/user-attachments/assets/ea30c0df-6755-4b5c-aef4-b6c48bb92eb0" />

#### Remote Backend
<img width="1391" height="715" alt="image" src="https://github.com/user-attachments/assets/dd5f8809-7f24-4834-9f0e-5bd87c23544a" />
<img width="1475" height="771" alt="image" src="https://github.com/user-attachments/assets/ab7d0288-45b5-46b1-a5d7-678effd56b95" />
<img width="993" height="521" alt="image" src="https://github.com/user-attachments/assets/190d1ebc-13a0-4c4c-8133-86e2f8469ba8" />
<img width="1016" height="458" alt="image" src="https://github.com/user-attachments/assets/c95b80a7-e490-4123-bb5a-6c3e4a117413" />

#### Bootstrapping
So we want to provision AWS objects with Terraform but Terraform remote Backend needs the resources; so it's a chicken and egg problem. 
What do we do then? We bootstrap by first keeping the provider locally first and create S3 Bucket and DynamoDB
<img width="977" height="506" alt="image" src="https://github.com/user-attachments/assets/0fc4ced4-0d80-442e-91b0-5e048c182b51" />
<img width="1001" height="565" alt="image" src="https://github.com/user-attachments/assets/2a12370f-f38d-44f5-a279-e45fc3476153" />
Then we perform `terraform apply` so S3 and DB are provisioned first.
<img width="1007" height="560" alt="image" src="https://github.com/user-attachments/assets/8a00aa6c-55df-4c42-b4fc-5a44c11cbe2d" />
So now our Terraform state file has those 2 resources
<img width="998" height="563" alt="image" src="https://github.com/user-attachments/assets/bccbfa26-c489-4533-bd66-2298601fc39c" />
Now we update the Terraform Backend to remote i.e. S3 and DynamoDB details:
<img width="1007" height="564" alt="image" src="https://github.com/user-attachments/assets/df91a1f5-7426-4199-98b6-dcb2d06cd287" />
<img width="930" height="556" alt="image" src="https://github.com/user-attachments/assets/5f70ea9f-d5c5-4667-9978-5f7bb7ba05ce" />
<img width="1009" height="556" alt="image" src="https://github.com/user-attachments/assets/2acdef1b-cf1c-40c0-bc56-9b23ff0350ad" />

## Part 4
### Variables and Outputs

#### Variable Types
- **Input Variables**
You can add variable blocks to your configuration to define input interface for your module. This lets users pass custom values to your module at runtime.
<img width="708" height="496" alt="image" src="https://github.com/user-attachments/assets/2e3813bb-75ee-43f2-82fc-4277eb0a39e4" />
<img width="990" height="541" alt="image" src="https://github.com/user-attachments/assets/d3218d06-2d23-4804-a7be-140d0de1915c" />
<img width="1045" height="553" alt="image" src="https://github.com/user-attachments/assets/bb3edeff-d937-42cc-a6a1-32469d606e29" />

- **Local Variables**
Local values are similar to function-scoped variables in other programming languages. Local values assign names to expressions, letting you use the name multiple times within a module instead of repeating that expression.

- **Output Variables**
Add output blocks to your configuration to expose information about your infrastructure on the command line, in HCP Terraform, and in other Terraform configurations. The output block serves the following purposes in Terraform:

  - Child modules can expose resource attributes to parent modules.
  - Root modules can display values in CLI output.
  - Other Terraform configurations using remote state can access root module outputs with the terraform_remote_state data source, including state sharing in HCP Terraform
  - Pass information from a Terraform operation to an automation tool.
 
<img width="1467" height="759" alt="image" src="https://github.com/user-attachments/assets/53782441-c18e-493c-bd95-aacae05dae76" />

## Part 5
### Additional Language Features

<img width="984" height="527" alt="image" src="https://github.com/user-attachments/assets/bf4716ea-57fa-4734-b0d1-721f1fc27c31" />

#### Terraform Template Strings
Terraform template strings allow dynamic construction of text by embedding variables, expressions, and control structures within strings.

##### Key Features
- Interpolate variables and expressions using `${}` syntax.
- Generate dynamic resource names, tags, and configurations.
- Support conditional logic with `%{ if ... }` blocks.
- Support iteration with `%{ for ... }` loops.
- Improve reusability and reduce hardcoded values in configurations.
- Commonly used with `templatefile()` for external template files.

#### Terraform Operators
Terraform operators are symbols used to perform calculations, comparisons, and logical evaluations within expressions.

##### Key Features
- Arithmetic operators: `+`, `-`, `*`, `/`, `%`.
- Comparison operators: `==`, `!=`, `<`, `>`, `<=`, `>=`.
- Logical operators: `&&`, `||`, `!`.
- Used in conditions, variable assignments, and resource configurations.
- Enable dynamic and conditional infrastructure definitions.
- Commonly used with expressions and conditional statements.

#### Terraform Conditionals
Terraform conditionals enable decision-making within configurations by evaluating expressions and returning values based on specified conditions.

##### Key Features
- Use the ternary syntax: `condition ? true_value : false_value`.
- Dynamically assign values based on environment or input variables.
- Reduce duplication by handling multiple scenarios in a single expression.
- Commonly used in resource arguments, locals, and outputs.
- Improve flexibility and maintainability of infrastructure code.
- Support environment-specific and feature-based configurations.

#### Terraform For Expressions with Lists
Terraform for expressions with lists allow transformation, filtering, and generation of new lists from existing collections.

##### Key Features
- Iterate over list elements using the `for` expression syntax.
- Create new lists by transforming existing values.
- Support conditional filtering with `if` clauses.
- Reduce repetitive code when processing collections.
- Commonly used in locals, variables, and resource arguments.
- Improve readability and maintainability of list-based configurations.

#### Terraform Splat Expressions
Terraform splat expressions provide a concise way to access attributes from all elements in a collection of resources or objects.

##### Key Features
- Use the `[*]` syntax to extract values from multiple instances.
- Simplify access to attributes across lists of resources.
- Return a list containing the selected attribute values.
- Reduce the need for explicit `for` expressions in simple cases.
- Commonly used with resources created using `count` or collections of objects.
- Improve readability when working with repeated resource attributes.

#### Terraform Dynamic Block
Terraform dynamic blocks allow you to generate nested configuration blocks dynamically based on a collection of values.

##### Key Features
- Create repeated nested blocks without duplicating code.
- Iterate over lists, maps, or sets using the `for_each` argument.
- Simplify resource configurations with variable numbers of nested blocks.
- Improve reusability by making configurations more flexible.
- Commonly used for resources with multiple nested settings, such as security rules or disk configurations.
- Support conditional generation of nested blocks by controlling the input collection.

#### Terraform Constraints - Type and Version
Terraform constraints define variable data types and version requirements to ensure configuration consistency, compatibility, and predictable deployments.

##### Key Features
* Define variable types using `string`, `number`, `bool`, `list`, `map`, `set`, `object`, and `tuple`.
* Restrict the Terraform CLI version using the `required_version` argument.
* Specify compatible provider versions with the `required_providers` block.
* Support version constraint operators such as `=`, `!=`, `>`, `>=`, `<`, `<=`, and `~>`.
* Prevent incompatible Terraform or provider versions from being used.
* Improve configuration stability and consistency across environments.

#### Terraform Numeric Functions
Terraform numeric functions perform mathematical operations and numerical calculations within expressions.

##### Key Features
* Perform arithmetic and mathematical calculations on numeric values.
* Common functions include `abs()`, `ceil()`, `floor()`, `log()`, `max()`, `min()`, `pow()`, `signum()`, and `parseint()`.
* Support rounding, exponentiation, logarithms, and integer parsing.
* Enable dynamic calculations for resource configurations and variables.
* Frequently used in `locals`, variables, outputs, and resource arguments.
* Eliminate the need for external scripts to perform numeric computations.

#### Terraform String Functions
Terraform string functions manipulate, format, and transform text values within expressions.

##### Key Features
* Modify, combine, and format string values dynamically.
* Common functions include `chomp()`, `format()`, `formatlist()`, `indent()`, `join()`, `lower()`, `regex()`, `regexall()`, `replace()`, `split()`, `strcontains()`, `substr()`, `title()`, `trim()`, `trimprefix()`, `trimsuffix()`, `trimspace()`, and `upper()`.
* Support string formatting, pattern matching, and text replacement.
* Simplify resource naming, tagging, and output formatting.
* Frequently used in variables, `locals`, outputs, and resource arguments.
* Improve readability by reducing complex string manipulation logic.

#### Terraform Collection Functions
Terraform collection functions manipulate and transform lists, maps, sets, and other collection types within expressions.

##### Key Features
* Create, combine, filter, and transform collection values.
* Common functions include `alltrue()`, `anytrue()`, `chunklist()`, `coalescelist()`, `compact()`, `concat()`, `contains()`, `distinct()`, `element()`, `flatten()`, `index()`, `keys()`, `length()`, `lookup()`, `matchkeys()`, `merge()`, `one()`, `range()`, `reverse()`, `setintersection()`, `setproduct()`, `setsubtract()`, `setunion()`, `slice()`, `sort()`, `sum()`, `transpose()`, `values()`, and `zipmap()`.
* Support operations on lists, maps, sets, and tuples.
* Simplify data transformation for variables, locals, and outputs.
* Enable dynamic resource configuration using collection-based expressions.
* Reduce repetitive logic when working with complex data structures.

#### Terraform Encoding Functions
Terraform encoding functions convert data between different formats for serialization, parsing, and interoperability.

##### Key Features
* Encode and decode data in common formats.
* Common functions include `base64encode()`, `base64decode()`, `base64gzip()`, `csvdecode()`, `jsonencode()`, `jsondecode()`, `textencodebase64()`, `textdecodebase64()`, `urlencode()`, `yamlencode()`, and `yamldecode()`.
* Simplify data exchange with APIs, templates, and external services.
* Convert Terraform values to and from JSON, YAML, CSV, and Base64 formats.
* Commonly used for configuration files, user data scripts, and provider arguments.
* Eliminate manual serialization and parsing of structured data.

#### Terraform Filesystem Functions
Terraform filesystem functions read, process, and manage files and file paths within Terraform configurations.

##### Key Features
* Read file contents and process data from the local filesystem.
* Common functions include `abspath()`, `dirname()`, `pathexpand()`, `basename()`, `file()`, `fileexists()`, `fileset()`, `filebase64()`, `filebase64sha256()`, `filebase64sha512()`, `filemd5()`, `filesha1()`, `filesha256()`, `filesha512()`, `templatefile()`, and `csvdecode()`.
* Generate file hashes for integrity verification and change detection.
* Render templates with dynamic values using `templatefile()`.
* Simplify working with configuration files, scripts, and static assets.
* Commonly used for user data, cloud-init scripts, templates, and local configuration files.

#### Terraform Date and Time Functions
Terraform date and time functions generate, format, and manipulate date and time values within Terraform configurations.

##### Key Features
* Generate and format timestamps for resources and outputs.
* Common functions include `formatdate()`, `plantimestamp()`, `timeadd()`, and `timestamp()`.
* Format timestamps using custom date and time patterns.
* Perform date and time arithmetic by adding or subtracting durations.
* Commonly used for resource metadata, expiration dates, and automation workflows.
* Enable dynamic time-based values without external scripting.

#### Terraform Hash and Crypto Functions
Terraform hash and crypto functions generate cryptographic hashes and handle secure checksum operations for data integrity and validation.

##### Key Features
* Generate cryptographic hashes for strings and files.
* Common functions include `base64sha256()`, `base64sha512()`, `filemd5()`, `filesha1()`, `filesha256()`, `filesha512()`, `md5()`, `sha1()`, `sha256()`, and `sha512()`.
* Verify data integrity using consistent hashing mechanisms.
* Detect changes in files and configuration content.
* Support secure comparisons for immutable resources and caching.
* Commonly used in state validation, file change detection, and security-sensitive configurations.

#### Terraform IP Network Functions
Terraform IP network functions perform calculations and transformations on IP addresses and CIDR blocks for network configuration and allocation.

##### Key Features
* Calculate and manipulate IP address ranges and CIDR blocks.
* Common functions include `cidrhost()`, `cidrnetmask()`, `cidrsubnet()`, `cidrsubnets()`, and `cidrcontains()`.
* Derive host IPs from a given subnet using index-based allocation.
* Split larger CIDR blocks into smaller subnets for structured networking.
* Validate whether an IP address belongs to a specific CIDR range.
* Commonly used in VPC design, subnetting, and cloud networking configurations.

#### Terraform Type Conversion Functions
Terraform type conversion functions convert values between different data types to ensure compatibility in expressions and resource arguments.

##### Key Features
* Convert values between string, number, list, map, and set types.
* Common functions include `tostring()`, `tonumber()`, `tobool()`, `tolist()`, `toset()`, and `tomap()`.
* Ensure consistent data types across variables, locals, and outputs.
* Enable safe manipulation of dynamic or user-provided input values.
* Prevent type mismatch errors in Terraform configurations.
* Commonly used in variable validation, resource arguments, and data transformations.

<img width="995" height="561" alt="image" src="https://github.com/user-attachments/assets/aa4dadf6-1bf4-4ae8-b33e-94668857927c" />
<img width="991" height="542" alt="image" src="https://github.com/user-attachments/assets/b71b15b7-8a50-414a-b865-b74395646ba5" />
<img width="997" height="544" alt="image" src="https://github.com/user-attachments/assets/e751857f-8092-4d45-8d7d-2cb8fc407f07" />
<img width="981" height="546" alt="image" src="https://github.com/user-attachments/assets/c938d20c-8f16-4195-a21a-fd82b054f602" />
<img width="984" height="531" alt="image" src="https://github.com/user-attachments/assets/1b8ba872-4138-4fdc-a513-7f55041d759f" />

## Part 6
### Project Organization + Modules
<img width="975" height="534" alt="image" src="https://github.com/user-attachments/assets/46ab4bac-d2d2-4720-aced-7c1c865e5b41" />

#### Terraform Modules
Terraform modules are reusable packages of Terraform configurations that encapsulate related resources and logic to promote consistency, reusability, and scalability.

##### Key Features
* Encapsulate multiple resources into a single reusable unit.
* Improve code organization by separating concerns (network, compute, IAM, etc.).
* Support input variables (`variables.tf`) for customization.
* Expose outputs (`outputs.tf`) to pass data between modules.
* Enable composition by calling modules inside other modules (nested modules).
* Allow reuse from local paths, Git repositories, Terraform Registry, or remote sources.
* Promote standardization across environments (dev, staging, prod).
* Reduce duplication and improve maintainability in large infrastructures.

<img width="948" height="529" alt="image" src="https://github.com/user-attachments/assets/7885bd9f-d36a-4c10-8f7c-e10a2bf2b4d7" />

#### Terraform Types of Modules
Terraform modules are categorized based on how they are created, stored, and reused across infrastructure environments.

##### Key Features
* **Root Module**: The default working directory where Terraform is executed; defines the primary configuration.
* **Child Modules**: Reusable modules called from a root module or other modules to encapsulate specific functionality.
* **Local Modules**: Stored within the same repository using a local file path for tight coupling and quick development.
* **Remote Modules**: Stored in external sources like Git repositories, Terraform Registry, or HTTP URLs for reuse across projects.
* **Published Modules**: Versioned and shared via the Terraform Registry for standardized and community-driven usage.
* **Composable Modules**: Designed to be combined with other modules to build complex infrastructure systems.

<img width="949" height="533" alt="image" src="https://github.com/user-attachments/assets/bec599da-8644-4ea3-b904-d3f050da6833" />
<img width="1003" height="520" alt="image" src="https://github.com/user-attachments/assets/13371de0-e424-4ef4-b2da-8e454f00c376" />
<img width="984" height="530" alt="image" src="https://github.com/user-attachments/assets/9d480f39-31fd-4233-abd6-f196b563261d" />
<img width="986" height="546" alt="image" src="https://github.com/user-attachments/assets/ea140241-e8de-49b5-8875-6d666d9b186c" />
<img width="785" height="537" alt="image" src="https://github.com/user-attachments/assets/c4c83f84-450a-4be6-be17-52db1aa87ec4" />

## Part 7
### Managing Multiple Environments
<img width="987" height="543" alt="image" src="https://github.com/user-attachments/assets/f3840e5c-bc7f-4fe8-93b1-24271bd57aba" />
<img width="986" height="526" alt="image" src="https://github.com/user-attachments/assets/4ac752a3-f4f7-4ef1-8e09-b78bc75ed42a" />
<img width="996" height="551" alt="image" src="https://github.com/user-attachments/assets/c93e25b7-6578-4355-b77d-07f780f7fd94" />
<img width="987" height="552" alt="image" src="https://github.com/user-attachments/assets/c4a90e7a-34cc-4b65-bd32-0b2792bff0e0" />
<img width="992" height="555" alt="image" src="https://github.com/user-attachments/assets/32d570f2-977c-4f1d-adc5-0992a2a83927" />
<img width="981" height="476" alt="image" src="https://github.com/user-attachments/assets/3737d6d6-367f-4b53-b5ae-7f8aac8d4af1" />

#### Terraform Workspaces
Terraform workspaces allow you to manage multiple state files using the same Terraform configuration, making it easy to deploy identical infrastructure for different environments.

##### Key Features
* Each workspace maintains its own independent Terraform state.
* Reuse the same configuration for environments such as `dev`, `staging`, and `prod`.
* Switch between workspaces using Terraform CLI without modifying the configuration.
* Access the current workspace using `terraform.workspace` for environment-specific logic.
* Ideal when infrastructure is nearly identical across environments.
* Not a replacement for separate backends or projects when environments require different access controls or lifecycles.
* Default workspace is named `default`; additional workspaces can be created as needed.

##### Quick Commands
```bash
# List all workspaces
terraform workspace list

# Create a new workspace
terraform workspace new <workspace_name>

# Switch to a workspace
terraform workspace select <workspace_name>

# Show the current workspace
terraform workspace show

# Delete a workspace
terraform workspace delete <workspace_name>
```

#### Terraform File Structure for Multiple Environments
Instead of using workspaces, a common production approach is to maintain separate directories for each environment. Each environment has its own configuration, variables, and state while reusing shared modules.

##### Key Features
* Each environment (`dev`, `staging`, `prod`) has its own directory and independent state.
* Reuse common infrastructure through shared modules.
* Store environment-specific values in separate `terraform.tfvars` or variable files.
* Isolate deployments to reduce the risk of accidentally modifying another environment.
* Support different backends, providers, permissions, and resource configurations per environment.
* Preferred approach for production environments with different lifecycles, security, or compliance requirements.

##### Recommended Directory Structure
```text
terraform/
├── modules/
│   ├── network/
│   ├── compute/
│   └── storage/
│
├── environments/
│   ├── dev/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── terraform.tfvars
│   │   ├── backend.tf
│   │   └── outputs.tf
│   │
│   ├── staging/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── terraform.tfvars
│   │   ├── backend.tf
│   │   └── outputs.tf
│   │
│   └── prod/
│       ├── main.tf
│       ├── variables.tf
│       ├── terraform.tfvars
│       ├── backend.tf
│       └── outputs.tf
```

##### Workspaces vs Environment Directories
| Workspaces                                      | Environment Directories                                          |
| ----------------------------------------------- | ---------------------------------------------------------------- |
| Same configuration, multiple state files        | Separate configuration and state per environment                 |
| Best when environments are nearly identical     | Best when environments differ in size, permissions, or resources |
| Simpler for small projects                      | Preferred for production and enterprise projects                 |
| Shared backend configuration                    | Can use different backends for each environment                  |
| Higher risk of deploying to the wrong workspace | Better isolation and safer deployments                           |

## Part 8
### Testing Terraform Code
<img width="829" height="544" alt="image" src="https://github.com/user-attachments/assets/eccd9a39-40d1-4929-9f74-9d1d7b9f4ec5" />

<img width="990" height="560" alt="image" src="https://github.com/user-attachments/assets/ffffe835-98e2-4e98-aac0-3a65254e5ba3" />

<img width="770" height="495" alt="image" src="https://github.com/user-attachments/assets/41d4fcb7-6cbc-4727-86ee-13cfb054564b" />
<img width="969" height="531" alt="image" src="https://github.com/user-attachments/assets/c0167a70-396c-4b75-9d9d-952a2c4bad7b" />
<img width="888" height="541" alt="image" src="https://github.com/user-attachments/assets/f012f0cf-e953-42bb-bade-6a947f59afe2" />

## Part 8 - Demo
<img width="963" height="551" alt="image" src="https://github.com/user-attachments/assets/df685fec-e3bf-4ce9-85ff-a448838c85b6" />
<img width="815" height="573" alt="image" src="https://github.com/user-attachments/assets/1e1c4ac4-f3d6-47b6-9a49-8e81717b7611" />
<img width="1018" height="550" alt="image" src="https://github.com/user-attachments/assets/03a8163d-af64-4c81-8402-7c1fcdea77c6" />

## Part 9
### Developer Workflow
<img width="966" height="534" alt="image" src="https://github.com/user-attachments/assets/5828e4cc-afd2-4408-939b-a2888ecd3f29" />
<img width="983" height="522" alt="image" src="https://github.com/user-attachments/assets/6b2d142b-6d98-4906-8f95-fa14f2ae0606" />

### Additional Tools
<img width="990" height="545" alt="image" src="https://github.com/user-attachments/assets/551878ad-8479-4b85-8494-d0bcb9cc5835" />
<img width="972" height="537" alt="image" src="https://github.com/user-attachments/assets/39b45c91-774f-472d-9da6-5e6b746ba247" />

### CI/CD
<img width="972" height="537" alt="image" src="https://github.com/user-attachments/assets/7ca63e47-5558-4e44-af98-56a32398b75d" />

### Potential pitfalls
<img width="946" height="532" alt="image" src="https://github.com/user-attachments/assets/d8751098-7ddc-46a3-b944-683ad1a5b5db" />




























