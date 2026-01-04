# ☁️ Cloud Lab Setup: AWS & Azure Attackgrounds

**"The cloud is just someone else's computer. Learn how to own it."**

As cyber attacks increasingly target cloud environments, understanding how to simulate and exploit cloud vulnerabilities is critical. This document outlines the steps I followed to set up my lab for practicing cloud security.

---

## ☁️ Cloud Providers
You'll need an account with at least one of these. Most offer generous free tiers for learning.

- **AWS (Amazon Web Services):** The market leader. Their free tier is very generous for beginners.
    *   [AWS Free Tier](https://aws.amazon.com/free/)
    -   *Note:* You'll need a credit card for verification, but you won't be charged unless you exceed the limits. **Crucially, use a personal email, not your work one.**

- **Azure (Microsoft):** The second largest. They also offer free credits and services.
    *   [Azure Free Account](https://azure.microsoft.com/en-us/free/)
    -   *Note:* Similar credit card verification. Check country availability.

---

## 🚀 Setting Up Your Lab Environment
*The goal is to have a safe, isolated environment to practice attacking cloud resources.*

### 1. The Attack Machine (Your Base)
*   **Requirement:** You need a computer with **Bash/Zsh** (Linux/macOS) or **PowerShell** (Windows) and **sudo** privileges.
*   **Tools:**
    *   **Terraform:** The tool that automates cloud infrastructure. You'll use it to deploy the vulnerable lab.
        *   [Download Terraform](https://www.terraform.io/downloads.html)
    *   **AWS CLI:** For interacting with AWS programmatically.
        *   [Install AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)
    *   **Azure CLI:** For interacting with Azure programmatically.
        *   [Install Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
    *   **Docker:** For running pre-built environments (like CloudGoat).
        *   [Install Docker](https://docs.docker.com/get-docker/)

### 2. The Target Environment (The Lab)

Here's how I set up the labs:

#### **Scenario A: AWS Lab using CloudGoat**
*CloudGoat is a tool by Rhino Security Labs that simulates vulnerable AWS environments.*

1.  **Clone CloudGoat:**
    ```bash
    git clone https://github.com/RhinoSecurityLabs/cloudgoat.git
    cd cloudgoat
    ```
2.  **Install Dependencies:**
    ```bash
    pip3 install -r requirements.txt
    ```
3.  **Configure AWS Profile:**
    *   You need to set up your AWS credentials first.
    *   Run `aws configure` and enter the Access Key ID and Secret Access Key from your AWS IAM user (create a new user for this lab with minimal permissions, like `ReadOnlyAccess`).
    *   **Best Practice:** Create a separate IAM user with limited permissions just for lab work. Do NOT use your root AWS account.
    *   You can also use AWS profiles: `cloudgoat.py config profile <profile_name>`
4.  **Create a Scenario:**
    *   List available scenarios: `./cloudgoat.py list`
    *   Create a specific scenario (e.g., `iam_privesc_by_attachment`):
        ```bash
        ./cloudgoat.py create iam_privesc_by_attachment
        ```
    *   This will deploy the AWS resources (EC2, S3, IAM roles, etc.).
5.  **Destroy Resources:**
    *   After you finish, **clean up** to avoid charges!
    *   `./cloudgoat.py destroy` (for the current scenario)
    *   `./cloudgoat.py destroy --all` (to destroy everything)

#### **Scenario B: Azure Lab using PurpleCloud**
*PurpleCloud is another excellent tool for setting up Azure AD and IAM labs.*

1.  **Clone PurpleCloud:**
    ```bash
    git clone https://github.com/iknowjason/PurpleCloud.git
    cd PurpleCloud
    ```
2.  **Install Dependencies:**
    *   Check the `README.md` in the cloned repository for specific Python or Azure CLI requirements.
3.  **Login to Azure CLI:**
    ```bash
    az login
    ```
    *   Follow the prompts to authenticate through your browser.
4.  **Create Azure Resource Group:**
    ```bash
    az group create --name azuregoat_app --location eastus
    ```
5.  **Deploy with Terraform:**
    *   Navigate to the scenario directory (e.g., `azure_ad`).
    *   Initialize Terraform: `terraform init`
    *   Apply the configuration: `terraform apply --auto-approve`
    *   This will create users, groups, and applications in your Azure tenant.
6.  **Destroy Resources:**
    *   After you finish, run `terraform destroy --auto-approve` in the scenario directory to clean up.

---

## 🔑 Credentials for VMs
*When running the labs, you'll need these default credentials.*

*   **Windows VM (CloudGoat):**
    *   User: `ibuyauser`
    *   Password: `Password!`
*   **Linux VM (CloudGoat):**
    *   User: `fog`
    *   Password: `fog`
*   **Azure AD User (PurpleCloud):**
    *   Username: `harold.reed@<your-tenant-name>.onmicrosoft.com`
    *   Password: `Usable-arachnid-Fac8` (This will be generated, use the one from the output).

---

## 📚 Resources for Cloud Labs
*   [CloudGoat GitHub](https://github.com/RhinoSecurityLabs/cloudgoat)
*   [SadCloud GitHub](https://github.com/TBGSecurity/sadcloud)
*   [PurpleCloud GitHub](https://github.com/iknowjason/PurpleCloud)
*   [Terraform Documentation](https://developer.hashicorp.com/terraform/docs)
*   [AWS CLI Documentation](https://awscli.amazonaws.com/v2/documentation/api/latest/index.html)
*   [Azure CLI Documentation](https://docs.microsoft.com/en-us/cli/azure/get-started-with-azure-cli)
*   [OWASP Top 10](https://owasp.org/www-project-top-ten/)