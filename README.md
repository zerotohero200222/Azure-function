# Azure-function
# 🚀 Azure Function App Deployment with Terraform (Flex Consumption Plan)

This Terraform configuration deploys an **Azure Function App** using the **Flex Consumption Plan**, along with the necessary infrastructure including:

- Resource Group
- Storage Account and Blob Container
- Log Analytics Workspace (for Application Insights)
- Application Insights
- App Service Plan (Flex Plan)
- Azure Function App (Node.js, customizable)

---

## 📁 Project Structure

.
├── main.tf # Terraform infrastructure definitions
├── variables.tf # Input variables
├── outputs.tf # Outputs after deployment
├── providers.tf # Provider configurations
└── .github/workflows/
    └── terraform-deploy.yml # GitHub Actions CI/CD Pipeline

yaml
Copy
Edit

---

## 🛠️ Requirements

- Terraform >= 1.0
- Azure CLI or Azure Service Principal
- GitHub repository with secrets configured (see below)

---

## 🔐 GitHub Secrets Required

Configure these in your GitHub repository under:
**Settings → Secrets → Actions**

| Secret Name             | Description                         |
|-------------------------|-------------------------------------|
| `AZURE_CLIENT_ID`       | App registration client ID          |
| `AZURE_CLIENT_SECRET`   | App registration client secret      |
| `AZURE_TENANT_ID`       | Azure Active Directory tenant ID    |
| `AZURE_SUBSCRIPTION_ID` | Azure subscription ID               |

---

## 🚀 Deployment via GitHub Actions

This project uses **GitHub Actions** to automatically deploy the infrastructure when changes are pushed to the `main` branch.

### How it works:
- On every push to `main`:
  - Runs `terraform init`, `fmt`, `validate`, `plan`, and `apply`.
  - Deploys or updates your Azure Function App and dependencies.

---

## 📦 Usage

### 1. Clone the repo
git clone https://github.com/<your-org>/<your-repo>.git
cd <your-repo>
2. Customize runtime (Optional)
Edit variables.tf or terraform.tfvars to set runtime name and version:
runtime_name    = "node"
runtime_version = "20"
Other supported runtimes: dotnet-isolated, java, node, powershell, python

3. Manually Deploy (Optional)
You can also deploy manually using the CLI:
terraform init
terraform plan -out=tfplan
terraform apply tfplan
📤 Outputs
After deployment, you will get:

Resource Group name

Storage Account name

Function App name

Function App URL

📌 Notes
This deployment uses Flex Consumption Plan (FC1) which supports Linux only.

Application Insights is connected via a Log Analytics Workspace.

No remote backend is configured by default (state is local). For production, consider using Azure Storage backend.
