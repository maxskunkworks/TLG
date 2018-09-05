# TLG (Test Lab Guide) - Microsoft 365 + EMS (v1.0)

**Time to deploy**: Approx. 32 minutes

Last updated _9/4/2018_

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmaxskunkworks%2Ftlg%2Fmaster%2Ftlg-base-config_3-vm.m365-ems%2Fazuredeploy.json" target="_blank">
<img src="http://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fmaxskunkworks%2Ftlg%2Fmaster%2Ftlg-base-config_3-vm.m365-ems%2Fazuredeploy.json" target="_blank">
<img src="http://armviz.io/visualizebutton.png"/>
</a>

This template deploys the **TLG (Test Lab Guide) - Microsoft 365 + EMS**, a Test Lab Guide (TLG) configuration that represents a simplified intranet connected to the Internet and integrated with Microsoft 365 with EMS. This configuration is the starting point for additional TLGs that can be found [here](http://aka.ms/catlgs).

The **TLG (Test Lab Guide) - Microsoft 365 + EMS** provisions a Windows Server 2012 R2 or 2016 Active Directory domain controller using the specified domain name, an application server running Windows Server 2012 R2 or 2016, and a client VM running Windows Server 2016.

![alt text](images/tlg-m365-phase4.png "Diagram of the base config deployment")

## Usage

You can deploy this template in one of two ways:

+ Click the "Deploy to Azure" button to open the deployment UI in the Azure portal
+ Execute the PowerShell script at https://raw.githubusercontent.com/maxskunkworks/tlg/master/tlg-base-config_3-vm.m365-ems/scripts/Deploy-TLG.ps1 on your local computer.

## Solution overview and deployed resources

The following resources are deployed as part of the solution:

+ **ADDC VM**: Windows Server 2012 R2 or 2016 VM configured as a domain controller and DNS with static private IP address
+ **App Server VM**: Windows Server 2012 R2 or 2016 VM joined to the domain. IIS and .NET 4.5 are installed, and the directory C:\Files containing the file example.txt is shared as "\\APP1\Files" with full control for the User1 domain account.
+ **Client VM**: Windows Server 2016 client joined to the domain
+ **Storage account**: Diagnostics storage account, and client VM storage account if indicated. ADDC and App Server VMs in the deployment use managed disks, so no storage accounts are created for VHDs.
+ **NSG**: Network security group configured to allow inbound RDP on 3389
+ **Virtual network**: Virtual network for internal traffic, configured with custom DNS pointing to the ADDC's private IP address and tenant subnet 10.0.0.0/8 for a total of 16,777,214 available IP addresses.
+ **Network interfaces**: 1 NIC per VM
+ **Public IP addresses**: 1 static public IP per VM. Note that some subscriptions may have limits on the number of static IPs that can be deployed for a given region.
+ **JoinDomain**: Each member VM uses the **JsonADDomainExtension** extension to join the domain.
+ **BGInfo**: The **BGInfo** extension is applied to all VMs.
+ **Antimalware**: The **iaaSAntimalware** extension is applied to all VMs with basic scheduled scan and exclusion settings.

## Solution notes

+ All guest OS configuration is executed with DSC, using the resources CreateADPDC.ps1.zip and AppConfig.ps1.zip.
+ The domain user *User1* is created in the domain and added to the Domain Admins group. User1's password is the one you provide in the *adminPassword* parameter.
+ The *App server* and *Client* VM resources depend on the **ADDC** resource deployment in order to ensure that the AD domain exists prior to execution of the JoinDomain extensions for the member VMs. This asymmetric VM deployment process adds several minutes to the overall deployment time.
+ The private IP address of the **ADDC** VM is always *10.0.0.10*. This IP is set as the DNS IP for the virtual network and all member NICs.
+ The default VM size for all VMs in the deployment is Standard_D2_v2.
+ Deployment outputs include public IP address and FQDN for each VM.

`Tags: TLG, Test Lab Guide, Base Configuration`
___
Developed by the **MAX Skunkworks Lab**  
Author: Kelley Vice (kvice@microsoft.com)  
https://github.com/maxskunkworks

![alt text](images/maxskunkworkslogo-small.jpg "MAX Skunkworks")
