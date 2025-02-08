## Terraform - Infrastructure as Code (IaC)

### What is Terraform?
Terraform is an **Infrastructure as Code (IaC)** tool developed by **HashiCorp**.

- Automates infrastructure provisioning and eliminates manual setup of virtual machines (VMs), VPCs, subnets, and other cloud resources.
- Supports cloud providers like **AWS, Azure, GCP, Kubernetes**.
- Allows **one-click deployment** of multiple VMs (e.g., launching 10-20 instances simultaneously).
- Companies maintain Terraform templates in repositories like **GitHub** for quick deployments.

For more information, refer to the official Terraform documentation: [Terraform by HashiCorp](https://developer.hashicorp.com/terraform/intro)

### Why Use Terraform?
- **Automates Infrastructure Provisioning**
- **Reduces manual effort**
- **Faster deployments**
- **Cloud-agnostic** (works with AWS, Azure, GCP, etc.)
- **Infrastructure as Code (IaC)** approach (writing code to deploy infrastructure)

### Terraform vs. Ansible vs. AWS CloudFormation

| Feature              | Terraform            | Ansible                     | AWS CloudFormation |
|----------------------|---------------------|-----------------------------|--------------------|
| **Type**            | IaC & Provisioning  | Configuration Management & Provisioning | AWS-Specific IaC |
| **Primary Use**     | Infrastructure provisioning & configuration | Configuration Management & Provisioning | Automating AWS infrastructure |
| **Cloud-Agnostic?** | Yes (AWS, Azure, GCP) | Yes | No (AWS only) |
| **Declarative / Procedural** | Declarative | Procedural | Declarative |

### Terraform Key Points
- **Open-source** (developed by **HashiCorp**)
- **Works with AWS CloudFormation**
- **Supported on Windows 11**
- **Two main tasks:**
  - **Infrastructure Provisioning**
  - **Configuration Provisioning**

---

## Installing Terraform on Windows

### Step 1: Set Up IAM Access
1. Go to **AWS IAM Console**
2. Navigate to **Security Credentials**
3. **Create an Access Key**

### Step 2: Download and Configure Terraform
1. **Download** Terraform binary for Windows (ZIP file)
2. **Extract** the ZIP and rename the folder to `terraform`
3. **Move** the folder to `C:\soft\terraform`
4. **Set Environment Variables:**
   - System Variable → Path → Edit → New → Enter: `C:\soft\terraform`
   - Click OK, then close all dialog boxes

### Step 3: Verify Installation
1. Open **Command Prompt as Administrator**
2. Run:
   ```sh
   terraform -v  # Check Terraform version
   ```
3. If not recognized, navigate to the Terraform folder and open CMD there.
4. Run:
   ```sh
   terraform -h  # List available commands
   ```

### Alternative Installation (Linux)
```sh
apt install terraform
```

---

## Working with Terraform

### Step 1: Initialize Terraform
```sh
terraform init
```

### Step 2: Apply Configuration
```sh
terraform apply
```

---

## Example Terraform Configuration (AWS)
```hcl
provider "aws" {
  region     = "ap-south-1"
  access_key = "<YOUR_ACCESS_KEY>"
  secret_key = "<YOUR_SECRET_KEY>"
}
```
**Note:**
- Terraform files have a **.tf** extension.
- **Indentation is strict**, so be careful.

---

## Exploring Terraform Providers
- Visit **[Terraform Provider Registry](https://registry.terraform.io/)**
- Select a provider (e.g., Azure) to see available templates

---

## Conclusion
- Terraform is a **powerful IaC tool** that simplifies cloud infrastructure management.
- Enables **quick, automated deployments** across multiple cloud platforms.
- Companies use **predefined templates in GitHub** for efficiency.
- Works seamlessly with **AWS CloudFormation, Ansible, and Kubernetes**.

🚀 **Master Terraform and automate your cloud infrastructure today!**
