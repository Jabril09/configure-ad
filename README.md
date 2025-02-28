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
- Step 5 - Disable DC-1 firewall so client-1 can ping DC-1 without timing out.
- Step 6 - Install active dictory domain services on DC-1.
- Step 7 - Create organizational units and admin users in active directory.
- Step 8 - Create a Admin and normal user account in Active directory.
- Step 9 - Join Client-1 to your domain (mydomain.com)
- Step 10 - Sign in the admin account you created. This way we are showing you how you can sign into the same computer with different accounts because they are on the same domain.
- Step 11 - Set up remote desktop for non administrives on Client-1. 
- Step 12 -  Create additional users and attempt to log in Client-1 with one of the users you created. (OPTIONAL NO NEED TO CREATE USERS, JUST FOR PROJECT)
- Step 13 - Make sure to delete resource groups and VMs so you don't use your free credits. 



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
<img src="https://i.imgur.com/GC1MC0J.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
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
 Click static and save to set (NIC) of the domain controller. 
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
We are getting a reply back from DC-1 pretty cool right?.
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
<br /><img src="https://i.imgur.com/m45g7xT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From there click new file in top hand corner and name the file _EMPLOYESS. That why it will be easier to tell that you created the file. Do the same thing over to make the _ADMINS file then refresh the list.
</p>
<br /><img src="https://i.imgur.com/3ZJqYNg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After refreshing the list those files should be on top of the list.
</p>
<br /><img src="https://i.imgur.com/qRRVYcw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create another admin account. Click admins, new, user name jane doe or whatever name you want to put. Username jane_admin, create password and dont forget. Uncheck box and click password never expires and click finish. After that assign it to domain admin group. Right click name, properties, members of, click add. Type domain , click check names to see all the different groups. Join domain admins group to add. click apply then ok.
</p>
<br /><img src="https://i.imgur.com/gtbNLTH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click the windows button and type CMD (command Prompt).Command prompts allow you to use command phrases. Type in whoami to make sure you are in mydomain\labuser. From there type in logoff to logout. 
</p>
<br /><img src="https://i.imgur.com/an8zitH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to the portal to get DC-1 public IP address to sign back in as jane or whatever your mydomain.com name you created. Jane_admin and whatever password you created.
</p>
<br /><img src="https://i.imgur.com/X8h5tEw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now we are goin to join Client-1 to the domain. First we have to set Client-1 DNS (Domain Name Server) to DC-1 private IP address so they can join the domain controller because the domain controller knows what mydomain.com is. 
</p>
<br /><img src="https://i.imgur.com/eBTbezd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Sign into Client-1 as labuser by getting Client-1 public IP address and sign in remote desktop. Once signed in Command prompt and type in whoami or hostname to make sure you are signed into the Virtual Machine. 
</p>
<br /><img src="https://i.imgur.com/HGaMvjB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Right click start and go to systems. Click rename this pc (advanced). Click " to rename this computer or change it's domain or work group". Click members of domain.
</p>
<br /><img src="https://i.imgur.com/eIrW2q0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
DC-1 private IP address. Go back to the portal in azure and go to VM and click on DC-1. There you should find DC-1 private IP address. 
</p>
<br />
<br /><br /><img src="https://i.imgur.com/lxNymsT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to the portal in azure to get to Client-1. From there click networking then click network interface (NIC). Go to DNS server (domain name server) click custom to add DC-1 private IP address then click save. 
</p>
<br />

</p>
<br /><br /><img src="https://i.imgur.com/snyCdZ9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After saving DC-1 private IP address Client-1 will restart and flush the dns cache. 
</p>
<br /><br /><img src="https://i.imgur.com/RcjsvSQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log back in as Client-1 as original admin (labuser). Go to portal in azure and go to Client-1 and click restart. Click the windows start button and then type Command Prompt and type in IPconfigall to check new DNS server.
</p>
<br /><br /><img src="https://i.imgur.com/snyCdZ9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log in as mydomain.com jane_admin and whatever password you created. Click ok the computer will restart. Now we should be able to sign in as jane_admin in Client-1 desktop because they are on the same domain.
</p>
<br /><br /><img src="https://i.imgur.com/Pe7BSfr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now we are going to set up remote desktop so all normal domain users can remote into Client-1. Go to sytems then remote desktop settings. Select users that can remotely access this pc. 
</p>
<br />
<br /><br /><img src="https://i.imgur.com/dyCGvnz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In DC-1 go to tools to find active directory users and computers. then click mydomain.com and click users. 
</p>
<br />
<br /><br /><img src="https://i.imgur.com/kbJTRN4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now we see who all has access.
</p>
<br />
<br /><br /><img src="https://i.imgur.com/IO1Qtqh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
(EXTRA STEP: NO NEED TO CREATE RANDOM CLIENTS JUST FOR PROJECT)From here if not already logged into DC-1 log into DC-1 as Jane_admin (whatever name you created and password). Click the windows menue and open up the powershell ise as an admin. Right click powershell ise to open up as admin. Create a new file in powershell and paste the script that was given.
</p>
<br />
<br /><br /><img src="https://i.imgur.com/1t0oKlW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After pasting the previous script given. Hit run to run the script. Notice how it starting generating users. Within the script we pasted the password for the users is Password1.
</p>
<br />
<br /><br /><img src="https://i.imgur.com/NxTclfm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After populating the users, you can pick any user to try to sign in as one of the created users.
</p>
<br />
<br /><br /><img src="https://i.imgur.com/z1rXBYG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Copy and paste one of the generated names and open up remote desktop. Paste the name and type Password1 and see if you can sign in as one of the created users. 
</p>
<br />
<br /><br /><img src="https://i.imgur.com/6OCQeBO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once the credintials enetered you should see a screen like this with whatever name you decided to pick.
</p>
<br />
<br /><br /><img src="https://i.imgur.com/ozkZWQW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Please remember to delete all resources and VMs in azure so you do not waste your free credits.
</p>
<br />
