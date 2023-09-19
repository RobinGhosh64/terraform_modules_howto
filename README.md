# terraform_modules_howto
How to write a terraform module, that is easily callable by another caller module  


The root folder of this project has the main terraform module that creates a resource, key_vault and key_vault_access_policy.
It has variables.tf for variables it needs, some of which are defaults.

The key vault name is post fixed with -kv    ex. {name}-kv

The caller is an example in the example\simple folder. To test you need to be in that folder.


-- The azurerm_key_vault_access_policy is conditional and will be created/added to the key_vault VIA 'access_policies' attribute that can be passed directly from the caller as input. This is optional. 




How will you call the main module from your IAC code in the cloud?











How will you call the main module from your local?  Also, i want to pass in my access_policies.
