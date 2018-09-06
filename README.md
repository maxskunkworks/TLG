# Test Lab Guide (TLG) ARM Template Repository

The TLG repository contains ARM templates used to deploy Test Lab Guide (TLG) environments. You can learn more about TLGs [here](http://aka.ms/catlgs).

Azure Resource Manager (ARM)) templates are pre-configured prescriptive deployment packages that enable you to provision complex test/pilot environments in minutes that would otherwise require extensive PowerShell scripting or many hours of manual configuration. With little or no Azure experience, you can provision a standardized base environment for hands-on learning or to pilot integrated solutions.

## Templates

| Template                     | Name                                                    | Description
| :-------------------         | :-------------------                                    | :-------------------
| [tlg-base-config_3-vm](https://github.com/maxskunkworks/TLG/tree/master/tlg-base-config_3-vm) [<img src="http://azuredeploy.net/deploybutton.png">](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmaxskunkworks%2Ftlg%2Fmaster%2Ftlg-base-config_3-vm%2Fazuredeploy.json)        | 3 VM Base Configuration | This template deploys the **3 VM Base Configuration** base configuration that represents a simplified intranet connected to the Internet. This base configuration is the starting point for additional TLGs that can be found [here](http://aka.ms/catlgs).
| [tlg-base-config_3-vm.m365-ems](https://github.com/maxskunkworks/TLG/tree/master/tlg-base-config_3-vm.m365-ems) [<img src="http://azuredeploy.net/deploybutton.png">](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmaxskunkworks%2Ftlg%2Fmaster%2Ftlg-base-config_3-vm.m365-ems%2Fazuredeploy.json) | Simulated intranet for Microsoft 365 Test Lab Guides | This template deploys the **Simulated intranet for Microsoft 365 Test Lab Guides** base configuration that represents a simplified environment for Microsoft 365 Enterprise scenarios. This template corresponds to the [Simulated Enterprise Base Configuration](https://docs.microsoft.com/en-us/microsoft-365/enterprise/simulated-ent-base-configuration-microsoft-365-enterprise) Test Lab Guide.

All code in this repo is public (read-only to non-contributors). All templates in the master branch of this repo have been tested and should deploy successfully, subject to limitations and known issues described in each template's README.

___
Developed by the **MAX Skunkworks Lab**

https://github.com/maxskunkworks

![MAX Skunkworks logo](https://github.com/oualabadmins/lab_deploy/blob/master/common/images/maxskunkworkslogo-small.jpg "MAX Skunkworks")

Last update: _9/6/2018_