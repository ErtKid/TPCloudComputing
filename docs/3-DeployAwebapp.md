[Back to Home](../README.md)

# Deploy a Web App

![Alt text](image-3.png)
![Alt text](image-4.png)
![Alt text](image-5.png)

## Export template

```
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "sites_TPCloudComputing1_name": {
            "defaultValue": "TPCloudComputing1",
            "type": "String"
        },
        "serverfarms_TPCloudComputing1_externalid": {
            "defaultValue": "/subscriptions/ab2abc0e-cb01-45b4-a1ed-e1d90a67e6c5/resourceGroups/TPCloudComputing1QS-rg/providers/Microsoft.Web/serverfarms/TPCloudComputing1",
            "type": "String"
        }
    },
    "variables": {},
    "resources": [
        {
            "type": "Microsoft.Web/sites",
            "apiVersion": "2023-01-01",
            "name": "[parameters('sites_TPCloudComputing1_name')]",
            "location": "East US",
            "kind": "app,linux",
            "properties": {
                "enabled": true,
                "hostNameSslStates": [
                    {
                        "name": "tpcloudcomputing1.azurewebsites.net",
                        "sslState": "Disabled",
                        "hostType": "Standard"
                    },
                    {
                        "name": "tpcloudcomputing1.scm.azurewebsites.net",
                        "sslState": "Disabled",
                        "hostType": "Repository"
                    }
                ],
                "serverFarmId": "[parameters('serverfarms_TPCloudComputing1_externalid')]",
                "reserved": true,
                "isXenon": false,
                "hyperV": false,
                "vnetRouteAllEnabled": false,
                "vnetImagePullEnabled": false,
                "vnetContentShareEnabled": false,
                "siteConfig": {
                    "numberOfWorkers": 1,
                    "linuxFxVersion": "NODE|20-lts",
                    "acrUseManagedIdentityCreds": false,
                    "alwaysOn": false,
                    "http20Enabled": false,
                    "functionAppScaleLimit": 0,
                    "minimumElasticInstanceCount": 0
                },
                "scmSiteAlsoStopped": false,
                "clientAffinityEnabled": true,
                "clientCertEnabled": false,
                "clientCertMode": "Required",
                "hostNamesDisabled": false,
                "customDomainVerificationId": "D4F60F782D279FBDA2B65C3A627A5D84A53799B4843CF1F5A8F17AD89B3CAE93",
                "containerSize": 0,
                "dailyMemoryTimeQuota": 0,
                "httpsOnly": false,
                "redundancyMode": "None",
                "storageAccountRequired": false,
                "keyVaultReferenceIdentity": "SystemAssigned"
            }
        },
        {
            "type": "Microsoft.Web/sites/basicPublishingCredentialsPolicies",
            "apiVersion": "2023-01-01",
            "name": "[concat(parameters('sites_TPCloudComputing1_name'), '/ftp')]",
            "location": "East US",
            "dependsOn": [
                "[resourceId('Microsoft.Web/sites', parameters('sites_TPCloudComputing1_name'))]"
            ],
            "properties": {
                "allow": true
            }
        },
        {
            "type": "Microsoft.Web/sites/basicPublishingCredentialsPolicies",
            "apiVersion": "2023-01-01",
            "name": "[concat(parameters('sites_TPCloudComputing1_name'), '/scm')]",
            "location": "East US",
            "dependsOn": [
                "[resourceId('Microsoft.Web/sites', parameters('sites_TPCloudComputing1_name'))]"
            ],
            "properties": {
                "allow": true
            }
        },
        {
            "type": "Microsoft.Web/sites/config",
            "apiVersion": "2023-01-01",
            "name": "[concat(parameters('sites_TPCloudComputing1_name'), '/web')]",
            "location": "East US",
            "dependsOn": [
                "[resourceId('Microsoft.Web/sites', parameters('sites_TPCloudComputing1_name'))]"
            ],
            "properties": {
                "numberOfWorkers": 1,
                "defaultDocuments": [
                    "Default.htm",
                    "Default.html",
                    "Default.asp",
                    "index.htm",
                    "index.html",
                    "iisstart.htm",
                    "default.aspx",
                    "index.php",
                    "hostingstart.html"
                ],
                "netFrameworkVersion": "v4.0",
                "linuxFxVersion": "NODE|20-lts",
                "requestTracingEnabled": false,
                "remoteDebuggingEnabled": false,
                "httpLoggingEnabled": true,
                "acrUseManagedIdentityCreds": false,
                "logsDirectorySizeLimit": 100,
                "detailedErrorLoggingEnabled": false,
                "publishingUsername": "$TPCloudComputing1",
                "scmType": "None",
                "use32BitWorkerProcess": true,
                "webSocketsEnabled": false,
                "alwaysOn": false,
                "managedPipelineMode": "Integrated",
                "virtualApplications": [
                    {
                        "virtualPath": "/",
                        "physicalPath": "site\\wwwroot",
                        "preloadEnabled": false
                    }
                ],
                "loadBalancing": "LeastRequests",
                "experiments": {
                    "rampUpRules": []
                },
                "autoHealEnabled": false,
                "vnetRouteAllEnabled": false,
                "vnetPrivatePortsCount": 0,
                "localMySqlEnabled": false,
                "ipSecurityRestrictions": [
                    {
                        "ipAddress": "Any",
                        "action": "Allow",
                        "priority": 2147483647,
                        "name": "Allow all",
                        "description": "Allow all access"
                    }
                ],
                "scmIpSecurityRestrictions": [
                    {
                        "ipAddress": "Any",
                        "action": "Allow",
                        "priority": 2147483647,
                        "name": "Allow all",
                        "description": "Allow all access"
                    }
                ],
                "scmIpSecurityRestrictionsUseMain": false,
                "http20Enabled": false,
                "minTlsVersion": "1.2",
                "scmMinTlsVersion": "1.2",
                "ftpsState": "FtpsOnly",
                "preWarmedInstanceCount": 0,
                "elasticWebAppScaleLimit": 0,
                "functionsRuntimeScaleMonitoringEnabled": false,
                "minimumElasticInstanceCount": 0,
                "azureStorageAccounts": {}
            }
        },
        {
            "type": "Microsoft.Web/sites/hostNameBindings",
            "apiVersion": "2023-01-01",
            "name": "[concat(parameters('sites_TPCloudComputing1_name'), '/', parameters('sites_TPCloudComputing1_name'), '.azurewebsites.net')]",
            "location": "East US",
            "dependsOn": [
                "[resourceId('Microsoft.Web/sites', parameters('sites_TPCloudComputing1_name'))]"
            ],
            "properties": {
                "siteName": "TPCloudComputing1",
                "hostNameType": "Verified"
            }
        }
    ]
}
```
