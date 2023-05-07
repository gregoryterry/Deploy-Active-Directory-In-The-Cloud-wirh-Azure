# Deploy and Configure Active Directory In The Cloud wirh Azure
This lab will demostrate how to create and configure Azure virtual machines to install Windows Server and promote the server to a domain controller.
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


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


<h4>Create the Domain Controller VM and Resource Group (Windows Server 2022) Named “DC01</h4>

</p>Log in to Azure at:	portal.azure.com

In the search bar type:  virtual machines

[+] Create > Azure Virtual Machines
</p>
<img src="https://imgpile.com/images/haxOCx.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Use the current subscription

Select Create new Resource Group > Name: AD-Lab-01

Virtual Machine Name:  DC-1

Select a Region:  (US) West US 3
</p>
<img src="https://imgpile.com/images/haxAeL.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Select Security type: Standard

Select and Image:  Windows Server Datacenter

Select Size:  select a size that fits your need
<p>
<img src="https://imgpile.com/images/haxk8j.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Create username and password for the Administrator account

Make sure Inbound port (3389) RDP is checked
<p>
<img src="https://imgpile.com/images/hax06o.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Check the Licensing and Confirm check boxes > click next
<p>
<img src="https://imgpile.com/images/haxBRC.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

<p>Use the default disk settings > next
<p>
<img src="https://imgpile.com/images/haxFcS.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Leave the default settings for Networking > Review + create
<p>
<img src="https://imgpile.com/images/haxQB8.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>When validation passes > create
<p>
<img src="https://imgpile.com/images/hax3M3.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>When deployment is complete, go to resource
<p>
<img src="https://imgpile.com/images/haxvub.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>


<h4>Set the NIC for DC01 Private IP address to static</h4>

<p>This is the DC-1 private IP address 10.0.0.4

Select:  Settings > Networking
</p>
<img src="https://imgpile.com/images/haK4F4.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Click on DC-1 Network interface interface
<p>
<img src="https://imgpile.com/images/haxyfM.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>IP configurations >  Private IP address
<p>
<img src="https://imgpile.com/images/haxjRk.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Change to Static >  save
<p>
<img src="https://imgpile.com/images/haK1u2.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>DC-1 private IP 10.0.0.4 is now set to static
<p>
<img src="https://imgpile.com/images/haKIJG.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>


<h4>Create the Client VM (Windows 10) named “GTWS-01”</h4?\>

</p>Type Virtual machines in the search bar >

Create [+] > Azure Virtual Machine
</p>
<img src="https://imgpile.com/images/haKdFc.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>


</p>Add the client VM  to the same Resource Group

Give the Client VM a name:  GTWS-01

Put the client VM  in the same region:  West US 3
</p>
<img src="https://imgpile.com/images/haKTTR.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>


</p>Security type:  Standard

Image: Windows 10 Pro

Size:  Standard_E2S _V3  16 gig

**select the size that will fit your needs
</p>
<img src="https://imgpile.com/images/haKbfg.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

</p>Administrator account

Username:	gregory.terry

Password: 

Allow the selected port for RDP (3389)
</p>
<img src="https://imgpile.com/images/haK97N.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Check the Licensing box  >  click next until you get to networking
<p>
<img src="https://imgpile.com/images/haKCJW.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

<p>DC-1 and GTWS-01 are attached to the same subnet
<p>
<img src="https://imgpile.com/images/haKDLP.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Create
<p>
<img src="https://imgpile.com/images/haKGy1.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

</p>When validation and deployment are complete,
type Virtual machines in the search bar and you
will see DC01 and GTWS-01 virtual machines.
</p>
<img src="https://imgpile.com/images/haKxDL.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>


<h4>Logon to the Client VM with Remote Desktop</h4>

</p>Log into GTWS-01 with Remote Desktop using the public IP address

Click GTWS-01 VM, copy the public IP address
</p>
<img src="https://i.imgur.com/BeTYgJP.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

</p>Open Remote Desktop from your personal computer
or from inside the Client VM Paste the public IP address
for GTWS-01 Enter a username > connect
</p>
<img src="https://i.imgur.com/Dx0doDd.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

<p>Enter your password for the client VM
<p>
<img src="https://i.imgur.com/bqkV4Xa.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>


<h4>Enable ICMP in the DC01 Firewall and Test Connectivity Between GTWS-01 and DC01</h4>

<p>Here is the desktop for the client VM
<p>
<img src="https://i.imgur.com/LFuPwTa.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>
Right-click the start menu > Select Run > type CMD

to open a command prompt
<p>
<img src="https://i.imgur.com/mHfa7fV.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
  
</p>Ping the private address of DC01	<b>ping 10.0.0.4</b>

**if you get a reply, that means that the client VM can communicate with DC-1

** if you get a “request timed out”, you will have to enable ICMP in the  DC-1 firewall
</p>
<img src="https://i.imgur.com/ikg8sCr.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>

<p>Use Remote Desktop to log on to DC-1 with the public IP address

<img src="https://i.imgur.com/0QRVKy5.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

<p>Enter your password for DC01
<p>
  <img src="https://i.imgur.com/2BJdhNg.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
  
<p>I am logged into DC01 and we can see Server Manager console is open
<p>
  <img src="https://i.imgur.com/fy0GRaF.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  
<p>Go to the start menu > right-click > run > wf.msc
<p>
  <img src="https://i.imgur.com/bIOwwd0.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
  
<p>Select Inbound rules > sort by protocol >

look for ICMP > select these four
<p>
  <img src="https://i.imgur.com/N64777m.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Right-click each one and select enable rule
<p>
  <img src="https://i.imgur.com/abO4iPL.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  
</p>ICMP is now enabled on DC01

Go back to the client computer, try to ping the private address 10.0.0.4 for DC01

	<b>Ping 10.0.0.4</b>
	
It works because I changed the inbound rule on the DC-1 firewall to accept ICMP traffic
</p>
  <img src="https://i.imgur.com/BqiS6ug.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
  

<h4>Install Active Directory Domain Services</h4>

<p>Log on to DC01

In Server Manager > Manage > Add Roles and Features
<p>
  <img src="https://i.imgur.com/7PdnlfT.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  
<p>Role based or Feature-based installation
<p>
  <img src="https://i.imgur.com/kx08wlK.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  
<p>Destination Server:  Select Server from server pool

Server Name:  DC01
<p>
  <img src="https://i.imgur.com/NY328Uq.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  
<p>Select:  Active Directory Domain Services
<p>
  <img src="https://i.imgur.com/pbSjQJM.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  
<p>Select:  Add Features
<p>
  <img src="https://i.imgur.com/0kQvlxT.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
  
<p>Next
<p>
  <img src="https://i.imgur.com/QlfIF2M.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  
<p>Click next until you get to the install screen > install
<p>
  <img src="https://i.imgur.com/4vLfGB4.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  
<p>Active Directory is installing on DC01,
when complete, close the wizard
<p>
  <img src="https://i.imgur.com/k9LYy3v.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  

<h4>Promote DC01 to a Domain Controller</h4>
  
<p>Click the yellow icon > select promote server to a domain controller
<p>
  <img src="https://i.imgur.com/SlKGNES.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  
</p>Deployment Configuration;  Add new Forest

**this is a new domain controller

Root name:	gterrylabdomain.com
</p>
  <img src="https://i.imgur.com/8uF41cq.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  
<p>Select the following options and specify a DSRM password for restore mode
<p>
  <img src="https://i.imgur.com/UTJqsrl.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  
<p>Click next until you get to the NetBios screen

Wait for the Netbios field to populate > click next
<p>
  <img src="https://i.imgur.com/7UV5Yjb.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  
<p>Click next until you reach the Prerequisites Check
When complete > click install
<p>  
  <img src="https://i.imgur.com/HVLZeso.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  
<p>Wait for the installation to complete.  You will be logged out automatically
<p>
<img src="https://i.imgur.com/3Qq5QH1.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
  
<p>Re-connect to the server with RDP

Using the FQDN, re-connect to DC01 with RDP

Gregterrylabdomain.com\gterrylab
<p>
<img src="https://i.imgur.com/vJgm38v.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
  
<p>Enter your password
<p>
<img src="https://i.imgur.com/nuSXLrU.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
  
</p>You are logged into the Domain controller

Go to the command prompt, type “whoami”

to see who you are logged in as.

Type “ hostname” to see what computer you are logged on to.
</p>
<img src="https://i.imgur.com/griTSMg.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
  
<p>You can see that I am logged into a domain “gterrylabdomain” as user “gterrylab”
<p>
<img src="https://i.imgur.com/Beajo4u.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
  

<h4> Create Organizational Units in the Domain Controller and Add a Domain Admin</h4>

<p>On DC01 > select tools > Active Directory Users and Computers
<p>
<img src="https://i.imgur.com/MoEiWgd.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
  
</P>Expand your domain > Right-click your domain > new > Organizational Unit
</P>
<img src="https://i.imgur.com/dDdXT2k.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<p>Give the new OU a name:	 <b>ADMINS</b>
<p>
<img src="https://i.imgur.com/4DMkrz4.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

<p>Use the same procedure to create a second OU, name it  EMPLOYEES

Here are the two OUs I created
<p>
<img src="https://i.imgur.com/UdcYxPn.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<h5>Create an Administrator Account</h5>

<p>Right-click ADMINS > new > user
<p>
<img src="https://i.imgur.com/67rPDbg.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

</p>Fill out the following fields:
first name > last name > full name >
user logon Full name >  click next
</p>
<img src="https://i.imgur.com/CFSSdfd.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

</p>Create a new Admin password

**you can enter a temporary password and check

“ user must change password at next logon” > next
</p>
<img src="https://i.imgur.com/2OzaE3z.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

<p>Finish
<p>
<img src="https://i.imgur.com/1XC0CQW.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

<p>Here is the new ADMIN user
<p>
<img src="https://i.imgur.com/WRrZ3lB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

<h5>Assign Greg Smith to the Administrators group</h5>

<p>Select Greg Smith > select the Member Of tab > add
<p>
<img src="https://i.imgur.com/2Gi21MM.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

<p>Type Administrators > check names > ok
<p>
<img src="https://i.imgur.com/qsIZ5dW.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

<p>Greg Smith is now a member of the Administrators group > ok
<p>
<img src="https://i.imgur.com/QIpQy8U.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

<p>Use the same method to create user “jane smith” inside the EMPLOYEES OU,
add her to the Domain Admins group
</p>

<img src="https://i.imgur.com/971Sfyo.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/GIgsoKl.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/Qu9aOtC.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/eEGucPa.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>


<p>Jane Smith was created inside the EMPLOYEES OU

Click Jane Smith > member of tab > add
<p>
<img src="https://i.imgur.com/61DfshY.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

<img src="" height="50%" width="50%" alt="Disk Sanitization Steps"/>

<p>Make Jane Smith a member of the Domain Admins group
<p>
<img src="https://i.imgur.com/Zzr8uKz.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/J65wCLJ.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>

<p?Log out and log in as Jane Smith
<p>
<img src="https://i.imgur.com/g1Vvt4g.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

<p>Enter the password
<p>
<img src="https://i.imgur.com/vQNAfOy.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

</p>After the login > run a cmd prompt > type “whoami”

this will show the user and domain you are logged into
</p>
<img src="https://i.imgur.com/0MCLZr8.png" height="30%" width="30%" alt="Disk Sanitization Steps"/>

<p>Type “hostname”  to see the host you are logged into
<p>
<img src="https://i.imgur.com/gQmqFbM.png" height="30%" width="30%" alt="Disk Sanitization Steps"/>

