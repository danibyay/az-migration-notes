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

Jenkins path of where the pipeline is run

> /var/lib/jenkins/workspace/pipeline_name_branch

## Caveats

The terraform pipeline relies on having dependencies ansible repos cloned. Using a null_resource and local provisioner I call a script that clones the repos.

That only needs to be done once, not every pipeline build, that's why the null_resource acting as an "existing" resource is very helpful.

However, when starting a new workspace in Jenkins, Jenkins doesn't have the cloned repos, so the trick is to taint the null_resource, so when Jenkins does a plan, realizes that it needs to build the *null_resource* and clone the repos in its own workspace.