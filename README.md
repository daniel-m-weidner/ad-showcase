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
<img src="https://i.imgur.com/ZfvqDv5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/jGQI5ws.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/raCl45t.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/TfzyKXQ.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now using the Public IP address from your client (Windows 10) VM, login to the machine and go through the windows usual prompts when starting a fresh Windows VM. It is time to ping our private webserver's private IP address. To do this, type "Powershell" in the Windows Search menu. You will see the command line open for you. The command is simply: ping xx(IP), [in my case ping 10.0.0.4]. You will see the ping response listed for you then. More information can be retrieved by entering [ipconfig /all]. You will see the DNS servers address being listed as the same address as well. This clearly indicates that the VM is able to connect to the webserver. Now we are ready to start configuring our Active Directory. To get started, close the current remote connection and connect to the AD Virtual Machine. The Server Manager will open again, and within, select "Add Roles and Features". A wizard will open, select "next" three times until you are in the "Server Roles" selection and tick "Active Directory Domain Services" and "next" again until you are able to select "Install", it will take a few moments. Close it and now you will notice an exclamation mark next to the flag icon in the top-right within Server Manager. There, you will now be able to "Activate" the Domain Controller. Click "Promote..."
</p>
<br />

<p>
<img src="https://i.imgur.com/g0xplnM.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/mtlcn3P.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/TfzyKXQ.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
Another Wizard will open up. Choose "Add New Forest". Choose a domain name (e.g. with .com) and a password. Make note of your domain name. Now keep clicking next within the wizard when possible and click "Install" when prompted. It will take a little while and a reboot will happen automatically. Simply reconnect to the VM after a minute and you're back in. 
