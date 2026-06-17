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

### State File
<img width="1472" height="779" alt="image" src="https://github.com/user-attachments/assets/a1c75fd1-e4d7-42f8-a707-302c8064a53e" />

#### Local Backend
<img width="905" height="510" alt="image" src="https://github.com/user-attachments/assets/ea30c0df-6755-4b5c-aef4-b6c48bb92eb0" />

#### Remote Backend
<img width="1391" height="715" alt="image" src="https://github.com/user-attachments/assets/dd5f8809-7f24-4834-9f0e-5bd87c23544a" />
<img width="1475" height="771" alt="image" src="https://github.com/user-attachments/assets/ab7d0288-45b5-46b1-a5d7-678effd56b95" />

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
