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
### Login to Azure: `az login`

Set env var to the subscription you want to use: export `AZURE_SUBSCRIPTION_ID=`
