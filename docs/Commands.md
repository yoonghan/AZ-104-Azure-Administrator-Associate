# Commands

## Azure CLI

1. PowerShell - [Command](https://learn.microsoft.com/en-us/powershell/azure/get-started-azureps)
2. Azure CLI - [Command](https://learn.microsoft.com/en-us/cli/azure/reference-index?view=azure-cli-latest)

```bash
az account show
```

```powershell
Get-AzSubscription
```

### Cloud shell 
- A session based portal that allows PowerShell or Azure CLI to be chosen.
- Exits in ~30mins. 
- Can upload/download/edit script in Cloud Shell storage stored at /home directory.
- Access at https://shell.azure.com

## Azure Resource Manager (ARM)

Topic is covered more in AZ-400.
[Template](https://learn.microsoft.com/en-us/azure/templates/)

```bash
az deployment group create \
  --name blanktemplate \
  --resource-group myResourceGroup \
  --template-file $templateFile
```

```powershell
New-AzResourceGroupDeployment `
  -Name blanktemplate `
  -ResourceGroupName myResourceGroup `
  -TemplateFile $templateFile
```
