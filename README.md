# kOps
[Releases](https://github.com/kubernetes/kops/releases/latest)
## Installation
```shell
brew update && brew install kops
```
### Linux:
```shell
curl -Lo kops https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
chmod +x kops
sudo mv kops /usr/local/bin/kops
```
### macOS
```shell
curl -Lo kops https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-darwin-amd64
chmod +x kops
sudo mv kops /usr/local/bin/kops
```
### Install Azure CLI
```shell
brew update && brew install azure-cli

or

curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```
### Login to Azure:
 `az login`

Set env var to the subscription you want to use if necessary: 
```shell
export `AZURE_SUBSCRIPTION_ID=...`
```
### Create a container & storage account in Azure Blob
```shell
az group create --name steve-kops-test --location eastus
az storage account create --name stevekopstest --resource-group steve-kops-test
export AZURE_STORAGE_ACCOUNT=stevekopstest
az storage account keys list --account-name stevekopstest
export AZURE_STORAGE_KEY="xxx..."
```
### Create a blob container
```shell
az storage container create --name steve-cluster-configs
az storage container list --output table
```
### Set the env var KOPS_STATE_STORE
`export KOPS_STATE_STORE=azureblob://steve-cluster-configs`
### Generate kOps SPN
`az ad sp create-for-rbac --name steve-kops-test --role owner --sdk-auth`

### Set corresponding env vars
```shell
export AZURE_TENANT_ID="xxx..."
export AZURE_CLIENT_ID="xxx..."
export AZURE_CLIENT_SECRET="xxx..."
```
### kOps commands
```shell
export KOPS_FEATURE_FLAGS=Azure
kops create cluster \
  --cloud azure \
  --name my-azure.k8s.local \
  --zones eastus-1 \
  --network-cidr 172.16.0.0/16 \
  --networking calico \
  --azure-subscription-id "${AZURE_SUBSCRIPTION_ID}" \
  --azure-tenant-id "${AZURE_TENANT_ID}" \
  --azure-resource-group-name steve-kops-test \
  --azure-route-table-name steve-kops-test \
  --azure-admin-user steve

az storage blob list --container-name steve-cluster-configs --output table
```


