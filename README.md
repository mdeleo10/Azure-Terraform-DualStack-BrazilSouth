# Azure-Terraform-DualStack-BrazilSouth

This Azure Terraform template creates a Dual Stack (IPv4/IPv6) Ubuntu latest version with the Active Directory Authentication for user login.

It has the following variables defined in the file variables.rf
- Resource Group Name
- Resource Region Location
- Admin Username
- Vnet Address Space
- Vnet Subnet Address Space

Guthub is setup for a workflow to to run Actions upon code change (push) and deploy/redploy as needed. 

## Prerequistes:

Action Secrets:
- AZURE_AD_CLIENT_ID (Service Principal)
- AZURE_AD_CLIENT_SECRET (Service Principal Password)
- AZURE_AD_TENANT_ID
- AZURE_SUBSCRIPTION_ID

### Note: The Service Principal needs to have the RBAC rights over the subscription to 
- Create a Resource Group
- Create a VM
- Create A Vnet and subnet
- Create Public IP addresses (IPv4 and IPv6)
- Create NSG

### Note 2: Also needed access to the existing Resource Group rg-terraform-state-001 for the following:
- Storage Account and IAM access, for example contributor, for cloudmdterraformstate in RG rg-terraform-state-001.
- Key Vault kv-terraform-script-001 in RG rg-terraform-state-001, with secret "sshIDpub" in the ssh public key string format example "ssh-rsa KKKKKKeyKKKKK userid@xxx.com". Note need to add IAM access, for example Key Vault Administrator to access and read keys 


## Adding support for Azure Active Directory to Azure Linux

See https://docs.microsoft.com/en-us/azure/active-directory/devices/howto-vm-sign-in-azure-ad-linux and https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_machine_extension

Optional based upon proper install of ssh Public Key
- ssh adminuser@VM-IP (will use ssh private key to login)

## See     .github/workflows/terraform.yml file for Action execution

# References:

- https://www.cloudninja.nu/post/2022/06/github-terraform-azure-part1/
- https://thomasthornton.cloud/2021/03/19/deploy-terraform-using-github-actions-into-azure/
- https://thomasthornton.cloud/2022/02/26/referencing-azure-key-vault-secrets-in-terraform/


