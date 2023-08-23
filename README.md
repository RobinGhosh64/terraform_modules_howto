# terraform_modules_howto
How to write a terraform module, that is easily callable by another caller module  


The root folder of this project has the main terraform module that creates a resource, key_vault and key_vault_access_policy.
It has variables.tf for variables it needs, some of which are defaults.

The Key_vault_name is post fixed with {name}-kv

The caller is an example in the exampe

The azurerm_key_vault_access_policy is conditional and will be created/added to the keyy_vault VIA access_policies attribute and can be passed directly from the caller as input/ but optional


The monitor diagnostics capabilities can be turned on by diagnostics variable


How to call the main module in your IAC code in the cloud
```terraform
module {
    source = "rghosh/key-vault/azurerm"
    version = "1.0.0"
}

inputs {
    name = "simple"
    resource_group_name = "simple-kv-rg"
    location = "eastus"
}
```
How to call the main module in your IAC code locally
It is recommended the to assign access using the `access_policies`variable.

```terraform
module {
    source = "rghosh/key-vault/azurerm"
    version = "1.0.0"
}

inputs {
    name = "simple"
    resource_group_name = "simple-kv-rg"
    location = "eastus"

    access_policies = [
        {
            object_id = "0000-0000-0000"
            certificate_permissions = ["get"]
            key_permissions = ["get"]
            secret_permissions  = ["get"]
            storage_permissions = []
        }
    ]
}
```
