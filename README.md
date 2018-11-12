# Test Lab Guide (TLG) ARM Template Repository

![TLG logo](https://github.com/oualabadmins/lab_deploy/blob/master/common/images/tlg.png "MAX Skunkworks")

The TLG repository contains ARM templates used to deploy Test Lab Guide (TLG) environments. TLGs help you quickly learn about Microsoft products. They're great for situations where you need to evaluate a technology or configuration before you decide whether it's right for you or before you roll it out to users. The "I built it out myself and it works" hands-on experience helps you understand the deployment requirements of a new product or solution so you can better plan for hosting it in production. You can learn more about TLGs [here](http://aka.ms/catlgs).

Azure Resource Manager (ARM) templates are pre-configured prescriptive deployment packages that enable you to provision complex test/pilot environments in minutes that would otherwise require extensive PowerShell scripting or many hours of manual configuration. With little or no Azure experience, you can provision a standardized base environment for hands-on learning or to pilot integrated solutions.

## TLG ARM Templates

| Template                     | Name                                                    | Description
| :-------------------         | :-------------------                                    | :-------------------
| [tlg-base-config_3-vm](https://github.com/maxskunkworks/TLG/tree/master/tlg-base-config_3-vm) [<img src="http://azuredeploy.net/deploybutton.png">](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmaxskunkworks%2Ftlg%2Fmaster%2Ftlg-base-config_3-vm%2Fazuredeploy.json)        | 3 VM Base Configuration | This template deploys the **3 VM Base Configuration** base configuration that represents a simplified intranet connected to the Internet. This base configuration is the starting point for additional TLGs that can be found [here](http://aka.ms/catlgs).
| [tlg-base-config_3-vm.m365-ems](https://github.com/maxskunkworks/TLG/tree/master/tlg-base-config_3-vm.m365-ems) [<img src="http://azuredeploy.net/deploybutton.png">](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmaxskunkworks%2Ftlg%2Fmaster%2Ftlg-base-config_3-vm.m365-ems%2Fazuredeploy.json) | Simulated intranet for Microsoft 365 Test Lab Guides | This template deploys the **Simulated intranet for Microsoft 365 Test Lab Guides** base configuration that represents a simplified environment for Microsoft 365 Enterprise scenarios. This template corresponds to the [Simulated Enterprise Base Configuration](https://docs.microsoft.com/en-us/microsoft-365/enterprise/simulated-ent-base-configuration-microsoft-365-enterprise) Test Lab Guide.

## Prerequisites

Before you deploy an ARM template in this repository, you need to have:

+ Access to an Azure subscription with sufficient resources to deploy the template. Most templates in this repository require the following available resources:

  + 12 cores (4 cores per VM)
  + 1 storage account

  **Note:** Trial subscriptions do not have sufficient available resources for deployment of these templates.
+ A supported browser for access to the Azure portal (https://portal.azure.com). For more information, see [Supported browsers and devices for the Azure portal](https://docs.microsoft.com/en-us/azure/azure-preview-portal-supported-browsers-devices).
+ A public domain name and administrative access to the domain's DNS records.

Some templates may have additional requirements specified in the template's README.

___

## Disclaimers

All code in this repo is public (read-only to non-contributors). All templates in the master branch of this repo have been tested and should deploy successfully, subject to limitations and known issues described in each template's README.

This project welcomes suggestions, but is currently closed to outside contributions. To report an issue, make a suggestion for additional templates, or to request updates to existing templates, please visit the [issues page](https://github.com/maxskunkworks/TLG/issues).

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
___
Developed by the **Office 365 Commercial Content Experience team**

Last update: _11/12/2018_