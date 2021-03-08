{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "virtualMachines_ARMvm_name": {
            "defaultValue": "ARMvm",
            "type": "String"
        },
        "disks_ARMvm_disk1_c5248130873243e2afb47c2a7066ba57_externalid": {
            "defaultValue": "/subscriptions/811c64c8-a770-471a-b3cf-e46fd311753d/resourceGroups/TEST/providers/Microsoft.Compute/disks/ARMvm_disk1_c5248130873243e2afb47c2a7066ba57",
            "type": "String"
        },
        "networkInterfaces_ARMvm_externalid": {
            "defaultValue": "/subscriptions/811c64c8-a770-471a-b3cf-e46fd311753d/resourceGroups/Test/providers/Microsoft.Network/networkInterfaces/ARMvm",
            "type": "String"
        }
    },
    "variables": {},
    "resources": [
        {
            "type": "Microsoft.Compute/virtualMachines",
            "apiVersion": "2019-07-01",
            "name": "[parameters('virtualMachines_ARMvm_name')]",
            "location": "eastus",
            "properties": {
                "hardwareProfile": {
                    "vmSize": "Standard_DS1_v2"
                },
                "storageProfile": {
                    "imageReference": {
                        "publisher": "MicrosoftWindowsServer",
                        "offer": "WindowsServer",
                        "sku": "2019-Datacenter",
                        "version": "latest"
                    },
                    "osDisk": {
                        "osType": "Windows",
                        "name": "[concat(parameters('virtualMachines_ARMvm_name'), '_disk1_c5248130873243e2afb47c2a7066ba57')]",
                        "createOption": "FromImage",
                        "caching": "ReadWrite",
                        "managedDisk": {
                            "id": "[parameters('disks_ARMvm_disk1_c5248130873243e2afb47c2a7066ba57_externalid')]"
                        }
                    },
                    "dataDisks": []
                },
                "osProfile": {
                    "computerName": "[parameters('virtualMachines_ARMvm_name')]",
                    "adminUsername": "userRoot",
					"adminPassword": "Parole_AZ97Parole8"
                    "windowsConfiguration": {
                        "provisionVMAgent": true,
                        "enableAutomaticUpdates": true
                    },
                    "secrets": [],
                    "allowExtensionOperations": true,
                    "requireGuestProvisionSignal": true
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[parameters('networkInterfaces_ARMvm_externalid')]"
                        }
                    ]
                }
            }
        }
    ]
}
