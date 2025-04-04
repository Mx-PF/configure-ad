<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" height="30%" width="70%"alt="Microsoft Active Directory Logo"/>
</p>

<h1>Preparing a Domain Cotroller & Active Directory Infrastructure</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>What is Needed</h2>
<h2>Environments and Technologies</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10

<h2>High-Level Deployment and Configuration Steps</h2>

Setup Domain Controller in Azure

- Create Resources
- Create a Virtual Network and Subnet
- Create a Domain Controller VM (Windows Server 2022)
- Log into the VM and and disable Windows Firewall (for testing connectivity)

Setup Client-1 in Azure

- Create the Client VM (Windows 10) named “Client-1” *(Username: labuser | Password: Cyberlab123!)*
- Attach it to the same region and Virtual Network as DC-1
- From the Azure Portal, restart Client-1
- Login to Client-1
- Attempt to ping DC-1’s private IP address
- From Client-1, open PowerShell and run ipconfig /all

<h2>Deployment and Configuration Steps</h2>
<br />
<br />
<h3 align="center">Setup Domain Controller in Azure</h3>
<br />
<p>
  Create the Resource group Named: 'Active-Directory-Lab'.
</p>
<p>
  <img src="https://i.imgur.com/2q1TFyp.png" height="75%" width="100%" alt="resource group"/>
</p>
<p>
  Create a Virtual Network and Subnet named: 'Active-Directory-VNet'.
</p>
<p>
  <img src="https://i.imgur.com/SyRpLJB.png" height="75%" width="100%" alt="vm windows"/>
</p>

Next we will Create the Domain Controller VM (*Windows Server 2022*) and call it: 'dc-1'.
<p>
Make sure everything is in the same region!
<p>
  <img src="https://i.imgur.com/Ims7lMA.png" height="75%" width="100%" alt="resource group"/>
<p>
Select any procerssing image with 2 or more CPUs.
<p>
Don't forget to fully agree to any Licensing or ToS (tesms of service).
<p>
For the username & password, we will use (Username: labuser | Password: Cyberlab123!).
</p>
  <img src="https://i.imgur.com/m40bDXm.png" height="75%" width="100%" alt="resource group"/>
<p>
For the networking section, make sure your vitual network is under 'Active-Directory-VNet'. 
<p>Then Review and create.
</p>
<img src="https://i.imgur.com/8LaLCS5.png" height="75%" width="100%" alt="resource group"/>
<p>
</p>
<br />
<h3 align="center">Setup Client-1 in Azure</h3>
<br />
<p> Start By creating a new VM called 'Client-1'.
<p> 
<img src="https://i.imgur.com/giOUGjN.png" height="75%" width="100%" alt="resource group"/>
<p> Windows image should be 'Windows 10 Pro, 22H2 - x64 Gen2'
<p>Also make sure to set a Username & Password, again for the sake of this guide I'd recomend the same credentials as before.
</p><img src="https://i.imgur.com/vUmIuhi.png" height="75%" width="100%" alt="resource group"/>
<p> You should see the Licensing/ToS text box at this point, make sure to accepte it to continue.
<p> 
<p> Click next until you reach the Networking section.
<p> Put Virtual Network to 'Active-Directory-VNet' and review and create.
<p> <img src="https://i.imgur.com/yps6reL.png" height="75%" width="100%" alt="resource group"/>
</p> Next go to dc-1's Network setting and IP configuraion page to set the IP to STATIC.
<p><img src="https://i.imgur.com/eKttlVr.png" height="75%" width="100%" alt="resource group"/>
</p> From now on the IP for dc-1 will never change regardless of reboots.
<p> The next step will log into dc-1 through remote desktop using the public IP, and dissable the firewall just for this lab.
 
Once logged in open 'Server Manager'. If do not see it, you might be in the wrong VM. or created the wrong VM type of VM (*IF the names match*)THE WINDOWS EDITION SHOULD SAY 'server' SIMILAR TO THIS.
<p> 
<img src="https://i.imgur.com/2dP7dfA.png" height="75%" width="100%" alt="resource group"/>
<p> If you see something similar for your end, then continue by pressing the Windows key + R and typing 'wf.msc' to bring up the firewall
<p> Once opened, click the red circle that says 'Windows defender firewall properties' And select off from the firewall state drop down menu in the red square.
Do the same for Domain, Private, and public profiles in the mini window. Hit aply when finnished
<p> <img src="https://i.imgur.com/9z8e0i8.png" height="75%" width="100%" alt="resource group"/>
<p>
  
</p> Next we will set client-1's DNS settings to DC-1's private IP address.

Within MS Azure you should see the private IP address under DC-1's VM overview. *Yours might be different from the picture*
<img src="https://i.imgur.com/0kreVKa.png" height="75%" width="100%" alt="resource group"/>
<p> 
Once you have the IP address copied, Follow this quick guide in order to change client-1's DNS settings
<p>
  
</p>

[Configure AD YouTube](https://youtu.be/-c2Q286xcTc) 
