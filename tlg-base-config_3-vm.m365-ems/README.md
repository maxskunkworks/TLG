# Simulated intranet for Microsoft 365 Test Lab Guides (v1.1)

**Time to deploy**: Approx. 32-40 minutes

Last updated _10/3/2018_

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmaxskunkworks%2Ftlg%2Fmaster%2Ftlg-base-config_3-vm.m365-ems%2Fazuredeploy.json" target="_blank">
<img src="http://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fmaxskunkworks%2Ftlg%2Fmaster%2Ftlg-base-config_3-vm.m365-ems%2Fazuredeploy.json" target="_blank">
<img src="http://armviz.io/visualizebutton.png"/>
</a>

This template deploys the **Simulated intranet for Microsoft 365 Test Lab Guides** base configuration that represents a a simplified environment for Microsoft 365 Enterprise scenarios. This template corresponds to the [Simulated Enterprise Base Configuration](https://docs.microsoft.com/en-us/microsoft-365/enterprise/simulated-ent-base-configuration-microsoft-365-enterprise) Test Lab Guide.

The **Simulated intranet for Microsoft 365 Test Lab Guides** template provisions a Windows Server 2012 R2 or 2016 Active Directory domain controller using the specified domain name, an application server running Windows Server 2012 R2 or 2016, and a client VM running Windows Server 2016. You can use the resulting environment to test the features and functionality of Microsoft 365 Enterprise, with additional Microsoft 365 Enterprise [Test Lab Guides](http://aka.ms/m365etlgs) or on your own.

![alt text](images/tlg-m365.png "Diagram of the base config deployment")

**Note:** You can choose to deploy the client VM with either _Windows Server 2016 Datacenter_ (the default choice), or _Windows 10 Pro_ if your Azure subscription is eligible for access to Windows 10 gallery images. The deployment will fail if you choose _Windows 10_ without an eligible subscription.

* For more information about eligible subscriptions, see https://docs.microsoft.com/en-us/azure/virtual-machines/windows/client-images#subscription-eligibility.

## Usage

You can deploy this template in one of two ways:

+ Click the **Deploy to Azure** button to open the deployment UI in the Azure portal
+ Execute the PowerShell script at https://raw.githubusercontent.com/maxskunkworks/tlg/master/tlg-base-config_3-vm.m365-ems/scripts/Deploy-TLG.ps1 on your local computer.

Prior to deploying the template, have the following information ready:

+ The public DNS domain name of your test environment (testlab.\<_your public domain_\>). Enter this name in the __Domain Name__ field after clicking the __Deploy to Azure__ button or for the value of the __domainName__ variable in the template parameters file.
+ A DNS label prefix for the URLs of the public IP addresses of your virtual machines. These URLs are generated for each virtual machine in your deployment in the format _\<DNS label prefix\>\<VM hostname\>.\<region\>.cloudapp.azure.com_. Enter this label in the __Dns Label Prefix__ field after clicking the __Deploy to Azure__ button or for the value of the __dnsLabelPrefix__ variable in the template parameters file.

After you deploy the template, you will need to complete the steps in [Phase 4](https://docs.microsoft.com/en-us/microsoft-365/enterprise/simulated-ent-base-configuration-microsoft-365-enterprise#phase-4-create-your-office-365-e5-and-ems-e5-subscriptions) in the [Simulated Enterprise Base Configuration](https://docs.microsoft.com/en-us/microsoft-365/enterprise/simulated-ent-base-configuration-microsoft-365-enterprise) Test Lab Guide article to complete the configuration.

## Solution overview and deployed resources

The following resources are deployed as part of the solution:

### VMs

+ **ADDC VM**: Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM configured as a domain controller and DNS with static private IP address
+ **App Server VM**: Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM joined to the domain. IIS and .NET 4.5 are installed, and the directory C:\Files containing the file example.txt is shared as "\\APP1\Files" with full control for the User1 domain account.
+ **Client VM**: Windows Server 2016 Datacenter or Windows 10 Pro client joined to the domain

### Storage

+ **Storage account**: Diagnostics storage account, and client VM storage account if indicated. ADDC and App Server VMs in the deployment use managed disks, so no storage accounts are created for VHDs.

### Networking

+ **NSG**: Network security group configured to allow inbound RDP on 3389
+ **Virtual network**: Virtual network for internal traffic, configured with custom DNS pointing to the ADDC's private IP address and tenant subnet 10.0.0.0/8 for a total of 16,777,214 available IP addresses.
+ **Network interfaces**: 1 NIC per VM
+ **Public IP addresses**: 1 static public IP per VM. Note that some subscriptions may have limits on the number of static IPs that can be deployed for a given region.

### Extensions

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

`Tags: TLG, Test Lab Guide, Base Configuration, M365, Microsoft 365`
___
Developed by the **MAX Skunkworks Lab**

https://github.com/maxskunkworks

![MAX Skunkworks logo](https://github.com/oualabadmins/lab_deploy/blob/master/common/images/maxskunkworkslogo-small.jpg "MAX Skunkworks")

## Changelog

+ **9/10/2018**: Original commit
+ **10/3/2018**: Updated to use friendly OS names