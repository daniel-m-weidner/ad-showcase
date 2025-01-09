<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Creating and Using an Active Directory (AD) with Azure Virtual Machines (VM's) </h1>

<h2>Operational Necessities</h2>

- Microsoft Azure (personal Virtual Machine platform of choice) (local VM optional)
- Remote Desktop
- Active Directory Domain Services 
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10

<h2>Steps involved in establishing and using your Active Directory</h2>

- Create two VMs, one running Windows Server 2022, another with Windows 10 (Azure)
- Configure NIC, DNS settings to link the AD with our client PC, testing
- 
<h2>Detailed Steps involved</h2>

<p>
<img src="https://i.imgur.com/y7SWUDn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/vMRZKk7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/advLZEt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
First, go to virtual machines within the Azure platform. Select "Create Azure Virutal Machine". Create a new resource group, if needed. The first VM will be the Active Directory with our Domain Controller. Thus, I will also name it accordingly for simplicity. Next, make sure you select the correct disk image, one of the Windows Server 2022 distributions. Make sure to use a size that will serve the purposes of this use case. Create your login credentials and make sure you make note of them. When finished, go ahead and select "Review and Create", and when finished loading, click "Create". Now the deployment has already begun. You can now go to Virtual Machines again and create the second Machine. Select the same resource group that was created, give it a fitting name, e.g. your name (this will be the client using the AD) select the Windows 10 image and set your login information again. Create the VM and while waiting for full deployment, we can configure the AD's NIC IP address to be static. Click on the Server VM within the Virtual Machines menu. Navigate to Networking -> Network settings. Click on the network Interface, which will open the IP settings. By selecting the ip config, you can now set the IP to be "Static" and "Save".
</p>
<br />

<p>
<img src="https://i.imgur.com/NZaH2Dc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/HqJCZ4r.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now go to the VM menu once more, it is time to boot into the Active Directory Domain Controller. Copy your Server VM's public IP address found there. Open the Remote Desktop program and input the IP. Enter your credentials when prompted. Windows will start and so will the server manager. For our purposes, we will need to turn off the firewall first to be able to experiment with our setup. Right-click on start, click "Run", and input wf.msc. Windows firewall will open. Select "Windows Defender Firewall Properties". Change the state to "Off", do the same for private and public profiles. Confirm with OK and close it. Now return to the Azure portal and click on the Server VM again. you will see the VM's private IP address displayed here, simply copy it. Now go to the other VM's settings, network settings and click on the NIC as before. One the left side, you will find "DNS servers" settings. Select "Custom", paste the IP address and "Save".
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
