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

