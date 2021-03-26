
# Azure Service principal

Use a service principal to connect to azure

key data
* SPN - service principal name
* App id or client id
* password or client secret
* tenant id
* subscription id

Command to show data about a service principal using the subscription id

> az ad sp show --id \<id>

Query all the service principals that there are in my subscription and only show the app id and tenant id

> az ad sp list --query "[].{id:appId, tenant:appOwnerTenantId}"

Change the active subscription

> az account set --subscription "Name of subscription"

List subscriptions

> az account list --output table

## Tips and Tricks

If the key data is saved in environment variables, use the file 

> source /home/user/.bashrc

or export them if it's temporal

> export AZURE_STUFF="lsdkjflsakjf"

If the password has the $ special character **it must be escaped**

> export AZURE_SECRET="@s8d7sf9\\$"
