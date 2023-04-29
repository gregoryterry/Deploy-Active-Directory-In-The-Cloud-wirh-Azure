# Deploy Active Directory In The Cloud wirh Azure
This lab will demostrate how to create and configure Azure virtual machines to install Windows Server and promote the server to a domain controller.
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2></h2>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create the Domain Controller VM and Resource Group (Windows Server 2022) Named “DC01
- Set the NIC for DC01 Private IP address to static
- Create the Client VM (Windows 10) named “GTWS-01”
- Logon to the Client VM with Remote Desktop
- Enable ICMP in the DC01 Firewall and Test Connectivity Between GTWS-01 and DC01
- Install Active Directory Domain Services
- Promote DC01 to a Domain Controller
- Create Organizational Units in the Domain Controller and Add a Domain Admin
- Configure DNS for Active Directory


<h4>Create the Domain Controller VM and Resource Group (Windows Server 2022) Named “DC01</h4>

<p>Log in to Azure at:	portal.azure.com

In the search bar type:  virtual machines

[+] Create > Azure Virtual Machines
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Use the current subscription
Select Create new Resource Group > Name: AD-Lab-01
Virtual Machine Name:  DC-1
Select a Region:  (US) West US 3
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Select Security type: Standard
Select and Image:  Windows Server Datacenter
Select Size:  select a size that fit your need
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Create username and password for the Administrator account
Make sure Inbound port (3389) RDP is checked
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Check the Licensing and Confirm check boxes > click next
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Use the default disk settings > next
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Leave the default settings for Networking > Review + create
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>When validation passes > create
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>When deployment is complete, go to resource
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<h4>Set the NIC for DC01 Private IP address to static</h4>

<p>This is the DC-1 private IP address 10.0.0.4
Select:  Settings > Networking
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Click on DC-1 Network interface interface
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>IP configurations >  Private IP address
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Change to Static >  save
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>DC-1 private IP 10.0.0.4 is now set to static
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>


<h4>Create the Client VM (Windows 10) named “GTWS-01”</h4?\>

<p>Type Virtual machines in the search bar >  Create [+] > Azure Virtual Machine
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Add the client VM  to the same Resource Group
Give the Client VM a name:  GTWS-01
Put the client VM  in the same region:  West US 3
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Security type:  Standard
Image: Windows 10 Pro
Size:  Standard_E2S _V3  16 gig	**select the size that will fit your needs
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Administrator account
Username:	gregory.terry
Password: 
Allow the selected port for RDP (3389)
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Check the Licensing box  >  click next until you get to networking
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>DC-1 and GTWS-01 are attached to the same subnet
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Create
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>DC-1 and GTWS-01 are attached to the same subnet
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>


<h4>Logon to the Client VM with Remote Desktop</h4>

<p>Log into GTWS-01 with Remote Desktop using the public IP address

Click GTWS-01 VM, copy the public IP address
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Open Remote Desktop from your personal computer or from inside the Client VM
Paste the public IP address for GTWS-01
Enter a username > connect
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Enter your password for the client VM
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<h4>Enable ICMP in the DC01 Firewall and Test Connectivity Between GTWS-01 and DC01</h4>

<p>Here is the desktop for the client VM
<p>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>


<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>
<img src="" height="70%" width="70%" alt="Disk Sanitization Steps"/>
