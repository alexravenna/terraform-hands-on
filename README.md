# terraform-hands-on
Hands on exercises for Terraform beginners.

# Workshop Exercises

## Basic resource creation and the write, plan, apply loop.

### Exercise 1.1: Creating a Basic Azure Resource Group
**Objective:** Learn how to define and create a basic Azure Resource Group using Terraform.

This exercise will guide you through the process of installing Terraform, configuring the Azure CLI, writing a Terraform configuration file to define an Azure Resource Group, initializing Terraform, planning the deployment, and applying the configuration to create the resource group in Azure.

**Tasks:**
1. Install Terraform and configure Azure CLI. [^1][^2]
2. Write a Terraform configuration file to define an Azure Resource Group. [^5]
3. Initialize Terraform and plan the deployment. [^7]
4. Apply the configuration to create the resource group in Azure. [^6]

### Exercise 1.2: Adding an Azure Storage Account
**Objective:** Expand the configuration to include an Azure Storage Account within the created Resource Group.

We will use the Storage Account to store Terraform state remotely in the next exercise. This exercise will guide you through the process of updating the Terraform configuration to include an Azure Storage Account and Container, planning and applying the changes, and verifying the creation of the Storage Account in the Azure portal.

**Tasks:**
1. Update the Terraform configuration to define an Azure Storage Account.
2. Add an Azure Storage Container to the Storage Account configuration.
3. Use Terraform to plan and apply the changes.
4. Verify the creation of the Storage Account in the Azure portal.

### Exercise 1.3: Start using git with Terraform
**Objective:** Learn how to use git to manage Terraform configurations and version control.

This exercise will guide you through the process of initializing a git repository in the directory where you have your Terraform configuration, adding a `.gitignore` file to exclude the `.terraform` directory and the `terraform.tfstate` file, and committing the Terraform configuration to the git repository. Please also take a look at the references for more information on which files to ignore when using git with Terraform.

1. Initialize a git repository in the directory where you have your Terraform configuration.
2. Add a `.gitignore` file to exclude the `.terraform` directory and the `terraform.tfstate` file. [^12]
3. Commit the Terraform configuration to the git repository.

### Bonus Exercises:
1. Add a `tags` block to the Resource Group and Storage Account configurations to apply metadata.
2. Use the terraform `show` command to inspect the current state of the Terraform-managed infrastructure.
3. Use the terraform `destroy` command to remove the resources created in the exercises and recreate them.
4. Create a remote git repository and push the Terraform configuration to it.


## Excercise 2 - Managing State and Remote Backends
### Exercise 2.1: Migrating State to Azure Remote Backend
**Objective:** Learn how to setup an Azure Storage Account for remote state management and to migrate Terraform state from local files to remote state.

**Tasks:**
1. Modify the Terraform configuration to use the Azure backend for state storage. [^3][^4] Concider renaming and recreating the resource group and storage account to have meaningful names before migrating the state.
2. Initialize Terraform with the new backend configuration and migrate the state with the appropriate `terraform init` option.
3. Observe the new `terraform.tfstate` file in the Azure Storage Account.

### Exercise 2.2: Add an existing resource to the Terraform configuration
1. Create a new resource group in the Azure portal, add some tags to it and create a Storage Account in it.
2. Create a terraform resource object that represents the existing resource group.
3. Use the `terraform import` command to import the existing resource group into the Terraform state. [^8]
4. Make sure you do not destroy, modify or recreate the existing resource group when running `terraform apply`.

### Bonus Exercises:
1. Use the `terraform taint` on the imported resource group to mark it for recreation.
2. Use the `terraform plan` command to see the changes that Terraform would apply to the imported resource group.
3. Use the `terraform apply` command to recreate the imported resource group.

### Exercise 3: Enhancing a Module with Variables and Outputs
**Objective:** Evolve an existing Terraform code into a module to use variables and outputs, making it more flexible and reusable.

Our plan is to refactor the existing Terraform configuration into a module, define input variables for resource names and other parameters, define outputs for important information like the Resource Group ID and Storage Account connection string, and use the module in the main Terraform configuration with variable values.

We are also planning to create different environments for our infrastructure, like `dev` and `stg`, and use the module in both environments with different configurations.

Our final directory structure might look something like this:

```
.
├── environments
│   ├── dev
│   │   ├── backend_override.tf
│   │   ├── provider_override.tf
│   │   └── terraform.tfvars
│   └── stg
│   │   ├── backend_override.tf
│   │   ├── provider_override.tf
│   │   └── terraform.tfvars
├── main.tf
├── variables.tf
├── outputs.tf
├── modules
│   ├── network
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   └── storage
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
└── terraform.tfvars
```

**Tasks:**
1. Refactor the existing Terraform configuration into a module.
2. Define input variables for resource names and other parameters, try to have a flexible but easy to use module with sane defaults.
3. Define outputs for important information like the Resource Group ID and Storage Account connection string.
4. Use the module in the main Terraform configuration with variable values.
5. Create a new deployment of your module that does not collide with the existing resources holding your terraform state.

### Exercise 5: Unique Resource Naming and Importing Existing Resources
**Objective:** Use the Terraform Random provider to avoid naming collisions and learn how to import existing Azure resources into Terraform management.

**Tasks:**
1. Integrate the Random provider to generate unique names for resources.
2. Create a new resource with a unique name and apply the configuration.
3. Identify an existing resource in Azure to be managed by Terraform.
4. Use Terraform's import command to bring the existing resource into Terraform state.
5. Modify the Terraform configuration to match the imported resource's settings.


# References

[^1]: [Install Terraform](https://learn.hashicorp.com/tutorials/terraform/install-cli)

[^2]: [Install Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)

[^3]:	[Terraform Azure Backend](https://developer.hashicorp.com/terraform/language/settings/backends/azurerm#example-backend-configurations)

[^4]: [Store Terraform state in Azure Storage](https://learn.microsoft.com/en-us/azure/developer/terraform/store-state-in-azure-storage)

[^5]: [Terraform Azure Resource Group](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/resource_group)

[^6]: [Terraform Apply Command](https://developer.hashicorp.com/terraform/cli/commands/apply)

[^7]: [Terraform Plan Comman](https://developer.hashicorp.com/terraform/cli/commands/plan)

[^8]: [Terraform Import Command](https://www.terraform.io/docs/cli/import/index.html)

[^9]: [Terraform Random Provider](https://registry.terraform.io/providers/hashicorp/random/latest/docs)

[^10]: [Terraform Variables](https://www.terraform.io/docs/language/values/variables.html)

[^11]: [Terraform Outputs](https://www.terraform.io/docs/language/values/outputs.html)

[^12]: [Terraform .gitignore](https://github.com/github/gitignore/blob/main/Terraform.gitignore)