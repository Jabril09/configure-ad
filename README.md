<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1 - Sign into portal.azure.com and create a resource group called AD-LAB
- Step 2 - Create a virtual machine (VM) and name it DC-1 for domain controller. Set the Network interface (NIC) private IP address to static of the domain controller. 
- Step 3 - Create another virtual machine (VM) for client 1 under the same resource group AD-LAB and same region. US west 3 , username labuser and password (whatever you created but do not forget it) 
- Step 4 - Ensure connectivity between DC-1 and client-1 with ping. Log into client-1 and ping DC-1. 
- Step 5 - Disable DC-1 firewall so client-1 can ping DC-1 without timing out
- Step 6 - Install active dictory domain services on DC-1
- Step 7 - Create organizational units and admin users in active directory.
- Step 8 - Create a Admin and normal user account in Active directory
- Step 9 - Join Client-1 to your domain (mydomain.com)
- Step 10 - 
- Step 11
- Step 12
- Step 13
- Step 14
- Step 15

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/BK3rDBI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Sign into Azure.
</p>
<br />

<p>
<img src="https://i.imgur.com/F8yOsDf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Make sure the resource group is in the same region as the (VMs).
</p>
<br />

<p>
<img src="https://i.imgur.com/v1Qu4jX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create the virtual machine (VM) DC-1. Select Windows servers 2022. Region US west 3. Click review and create.
</p>
<br />
<p>
<br /><img src="https://i.imgur.com/8CBrHpD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create the other virtual machine (VM) as Client-1. Select windows 10 and US region 3. Username labuser , password (whatever you created but dont forget) click review and create.
</p>
<br />
<img src="https://i.imgur.com/Y8rdbTC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to DC-1 and click on networking on the left side. Then click on the newtwork interface (NIC). To Change network interface (NIC).
</p>
<br />
<p>
<img src="https://i.imgur.com/fUPnSQ4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Then on the left side click ip configurations.
</p>
<br />
<p>
<img src="https://i.imgur.com/taPszWO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 click static and save to set (NIC) of the domain controller. 
</p>
<br />
<p>

<img src="https://i.imgur.com/hMBpKqO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To ensure connectivity between DC-1 and Client-1 get DC-1's private ip address. In azure go to DC-1 and the private ip address should be there on the right side almost at the middle of the page. Copy that address.
</p>
<br />
<p>
<img src="https://i.imgur.com/FuB2OYY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Open up Remote start in the start menu. After that put Client-1 public ip address in and sign into Client-1 via virtual machine you created. For the username type in labuser and the password you created.
</p>
<br />
<p>
<img src="https://i.imgur.com/3cJ9Iuo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Open up command prompt in the start menu. After that ping 10.0.0.4 ( DC-1 private ip address ) and notice has the ping timed out. It timed out because DC-1 firewall is up.
</p>
<br />
<p>
<img src="https://i.imgur.com/rVJn0oT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Sign into DC-1 the same as you would like Client -1. Get DC-1 public ip address from the azure portal. Then open up the windows start menu and type in remote desktop and paste DC-1 public ip address in and sign in as labuser and the password you created. After you are signed into DC-1 open up the windows start menu and type wf.msc for windows firewall. Click that and go to inbound runles on the left.
</p>
<br />
<p>
<img src="https://i.imgur.com/0ueQok4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click on protocol at the top of the list and look for ICMPv4 core networking. Expand the page to have a better view. Once you have found core networking expand it and enable core networking dianostics echo request. After open Client-1 back up and notice the difference. 
</p>
<br />
<p>
<img src="https://i.imgur.com/KFYX80T.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We are getting a reply back from DC-1 pretty cool.
</p>
<br />
<p>
<img src="https://i.imgur.com/AlmbwN5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now time to install Active Dicrectory on DC-1. Log into DC-1 and in service manager click "add roles and features".
</p>
<br />
<p>
<img src="https://i.imgur.com/dOyrDt4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After that click the yellow triangle in the upper right hand corner. Then click "promote the server as domain controller. Then add new forest name mydomain.com. Click next and make up a password that you will not forget. click next, next, next and compuer will restart (DC-1 will restart).
</p>
<br />
<p>
<img src="https://i.imgur.com/JRt9A3i.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now time to create organizational units and admin users. Once DC-1 restarts go back to azure and restart DC-1 because the ip address may have changed. Copy the ip address and sign in through remote desktop. In service manager go to tools at the top right hand of the corner and click active directory and computers. 
</p>
<br />
<img src="https://i.imgur.com/gVMigFy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Right click mydomain.com. Select new and then organizational unit. 
</p>
<br /><img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br /><img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br /><img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br /><img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br /><img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br /><img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br /><img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br /><img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br /><img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
