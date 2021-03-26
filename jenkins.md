# Jenkins

## Credentials

vault pass has to be a secret file

the rest can be secret text

## Azure SPN credentials with terraform

Usually terraform has two ways of connecting with an SPN

1. using terraform vars

2. using env vars.

For connecting with jenkins you have to go with option 2.

    ARM_SUBSCRIPTION_ID
    ARM_TENANT_ID
    ARM_CLIENT_ID
    ARM_CLIENT_SECRET

The provider file should look like this

    provider "azurerm" {
        features {}
        skip_provider_registration = true
    }