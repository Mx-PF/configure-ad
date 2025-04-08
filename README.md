<h1 align="center"> Preparing a Domain Cotroller & Active Directory Infrastructure in AZURE </h1> 

<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" height="30%" width="70%" alt="Microsoft Active Directory Logo"/>
</p>



<p align="center"> This guide shows you how to set up Active Directory using Azure Virtual Machines. </p> 
<p> 
<p> 
</p>


## Environments and Technologies
- Microsoft Azure (to create Virtual Machines)
- Remote Desktop (to connect to your Windows VM)
- Active Directory Domain Services
- PowerShell

## Operating Systems Used
- Windows Server 2022
- Windows 10

## Steps Overview
1. Set up a Domain Controller (dc-1) in Azure.
2. Set up a Client Machine (Client-1) in Azure.
3. Connect Client-1 to dc-1.

## Step-by-Step Instructions

### Step 1: Set Up the Domain Controller (dc-1) in Azure
- **Create a Resource Group**  
  In Azure, create a Resource Group named `Active-Directory-Lab`.  
  <img src="https://i.imgur.com/2q1TFyp.png" height="75%" width="100%" alt="resource group"/>

- **Create a Virtual Network**  
  In Azure, create a Virtual Network named `Active-Directory-VNet`. Set the region as the same for your resource group, click Review and create.
  <img src="https://i.imgur.com/SyRpLJB.png" height="75%" width="100%" alt="vm windows"/>

- **Create the Domain Controller VM (dc-1)**  
  In Azure, create a VM named `dc-1`. Use Windows Server 2022.  Agree to any licensing terms. Use the `Active-Directory-VNet` for the network. Review and create.  
  <img src="https://i.imgur.com/Ims7lMA.png" height="75%" width="100%" alt="resource group"/>  
  <p>Use Windows Server 2022 for the image, use the same region as your Resource Group, Choose a VM size of 2 or more CPUs.</p>
  
  Set the username to `labuser` and password to `Cyberlab123!`.
  <img src="https://i.imgur.com/m40bDXm.png" height="75%" width="100%" alt="resource group"/>  
  Use the `Active-Directory-VNet` for the network. Review and create.  
  <img src="https://i.imgur.com/8LaLCS5.png" height="75%" width="100%" alt="resource group"/>

- **Set dc-1’s IP to Static**  
  In Azure, go to dc-1’s Network settings, then IP configuration. Set the IP to static.  
  <img src="https://i.imgur.com/eKttlVr.png" height="75%" width="100%" alt="resource group"/>

- **Log into dc-1 and Turn Off the Firewall**  
  Use Remote Desktop to log into dc-1 with its public IP, username `labuser`, and password `Cyberlab123!`. Open Server Manager (THE WINDOWS EDITION SHOULD SAY 'server' SIMILAR TO THE Next Image).  
  <img src="https://i.imgur.com/2dP7dfA.png" height="75%" width="100%" alt="resource group"/>  
  Press Windows key + R, type `wf.msc`, and press Enter. Click “Windows Defender Firewall Properties.” Turn OFF the firewall state for Domain, Private, and Public profiles. Click Apply and OK next.
  <img src="https://i.imgur.com/9z8e0i8.png" height="75%" width="100%" alt="resource group"/>

---

### Step 2: Set Up Client-1 in Azure
- **Create the Client-1 VM**  
  In Azure, create a VM named `Client-1` using Windows 10 Pro, 22H2 - x64 Gen2. Use the same Resource Group and region as `dc-1`. 
  <img src="https://i.imgur.com/giOUGjN.png" height="75%" width="100%" alt="resource group"/>  
  Set the username to `labuser` and password to `Cyberlab123!`. Agree to licensing terms. 
  <img src="https://i.imgur.com/vUmIuhi.png" height="75%" width="100%" alt="resource group"/>  
  In the Networking section, use `Active-Directory-VNet`. Review and create.  
  <img src="https://i.imgur.com/yps6reL.png" height="75%" width="100%" alt="resource group"/>

- **Set Client-1’s DNS to dc-1’s Private IP**  
  In Azure, go to dc-1’s overview page to find its private IP address (e.g., 10.0.0.4). Copy it. Follow [this YouTube guide](https://youtu.be/-c2Q286xcTc) to change Client-1’s DNS settings to use dc-1’s private IP.  
  <img src="https://i.imgur.com/0kreVKa.png" height="75%" width="100%" alt="resource group"/>

- **Restart Client-1**  
  In Azure, go to Client-1’s overview page. Click the blue “Restart” button.  
  <img src="https://i.imgur.com/Km7XDxz.png" height="75%" width="100%" alt="resource group"/>

---

### Step 3: Connect Client-1 to dc-1
- **Log into Client-1**  
  In Azure, go to Client-1’s overview page. Copy its public IP address.  
  <img src="https://i.imgur.com/6gQm1pW.png" height="75%" width="100%" alt="resource group"/>  
  Use Remote Desktop to log into `Client-1` with the public IP, username `labuser`, and password `Cyberlab123!`. 
  <img src="https://i.imgur.com/K3n0L2h.png" height="75%" width="100%" alt="resource group"/>  
  <img src="https://i.imgur.com/C2hyb6y.png" height="75%" width="100%" alt="resource group"/>  
  I'd recommend saying “No” to all privacy prompts.  
  <img src="https://i.imgur.com/qjXtHya.png" height="75%" width="100%" alt="resource group"/>

- **Ping dc-1 from Client-1**  
  In Azure, go to `dc-1`’s overview page to find its private IP address (e.g., 10.0.0.4). Copy it.  
  <img src="https://i.imgur.com/HqZIFtd.png" height="75%" width="100%" alt="resource group"/>  
  On the `Client-1` VM, click the Windows icon, search for “PowerShell,” and open it.
  <img src="https://i.imgur.com/CWjjw1b.png" height="75%" width="100%" alt="resource group"/>  
  In PowerShell, type `ping 10.0.0.4` (replace with your `dc-1’s` private IP). Press Enter. You should see successful pings just like the image below.
  <img src="https://i.imgur.com/MflCnPx.png" height="75%" width="100%" alt="resource group"/>
If you see “destination host unreachable,” check `dc-1`’s firewall (it should ALL be off) or the IP address (It should match for your end, You might also get a different number than me).

- **Check Client-1’s DNS Settings**  
  In Client-1’s PowerShell, type `ipconfig /all` and press Enter. Scroll to the DNS Servers section. It should show dc-1’s private IP (e.g., 10.0.0.4). If it doesn’t, recheck dc-1’s firewall and the DNS settings.  
  <img src="https://i.imgur.com/pq97tvF.png" height="75%" width="100%" alt="resource group"/>

---

If everything Is similar to the images, congrats! Your Active Directory setup is complete!
