# Cloudera CDP Tools for Microsoft Azure

A set of tools to help use Cloudera CDP with Microsoft Azure:

## Azure quickstart template

ARM template that deploys essential Azure resources for Cloudera CDP environment.


<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fcegganesh84%2Fcdp-azure-tools%2Fmaster%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png" />
</a>

---

**Azure RM templates does not support role assignments at a scope other than resource group. So the
following role assignments need to be performed via CLI or UI.**

## Assumer identity role assignment

```bash
# Assign Managed Identity Operator role to the assumerIdentity principal at subscription scope
az role assignment create --assignee <prinicipal-id> --role 'f1a07417-d97a-45cb-824c-7a7467783830' --scope '/subscriptions/<subscription-id>'
# Assign Virtual Machine Contributor role to the assumerIdentity principal at subscription scope
az role assignment create --assignee <prinicipal-id> --role '9980e02c-c2be-4d73-94e8-173b1dc7cf3c' --scope '/subscriptions/<subscription-id>'
```

## Fine grained logger/dataAccess/ranger identity role assignment

```bash
# Assign Storage Blob Data Contributor role to the loggerIdentity principal at logs filesystem scope
az role assignment create --assignee <prinicipal-id> --role 'ba92f5b4-2d11-453d-a403-e96b0029c9fe' --scope "/subscriptions/<subscription-id>/resourceGroups/<rg-name>/providers/Microsoft.Storage/storageAccounts/<sa-name>/blobServices/default/containers/logs"
```

```bash
# Assign Storage Blob Data Owner role to the dataAccessIdentity principal at logs/data filesystem scope
az role assignment create --assignee <prinicipal-id> --role 'b7e6dc6d-f1e8-4753-8033-0f276bb0955b' --scope "/subscriptions/<subscription-id>/resourceGroups/<rg-name>/providers/Microsoft.Storage/storageAccounts/<sa-name>/blobServices/default/containers/data"
az role assignment create --assignee <prinicipal-id> --role 'b7e6dc6d-f1e8-4753-8033-0f276bb0955b' --scope "/subscriptions/<subscription-id>/resourceGroups/<rg-name>/providers/Microsoft.Storage/storageAccounts/<sa-name>/blobServices/default/containers/logs"
```

```bash
# Assign Storage Blob Data Contributor role to the rangerIdentity principal at data filesystem scope
az role assignment create --assignee <prinicipal-id> --role 'ba92f5b4-2d11-453d-a403-e96b0029c9fe' --scope "/subscriptions/<subscription-id>/resourceGroups/<rg-name>/providers/Microsoft.Storage/storageAccounts/<sa-name>/blobServices/default/containers/data"
```

---

## Azure quickstart template for cluster connectivity manager

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fcegganesh84%2Fcdp-azure-tools%2Fmaster%2Fazureccmdeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png" />
</a>

---

## Azure quickstart template for cluster connectivity manager with bastion host for magic SSO

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fcegganesh84%2Fcdp-azure-tools%2Fmaster%2Fazureccmbastiondeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png" />
</a>


# Changelog

1. Rename admin to dataAccess. (02/20/2020)
