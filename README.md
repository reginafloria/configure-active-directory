<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://youtu.be/SkkEpnaYac8)
<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create a bunch of additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>
 
<p>
<img src="https://imgur.com/Jifz0RI.jpg" height="80%" width="80%" alt="Screenshot of Server DC-1 and Client-1"/>
</p>
<p>
Creation of the Server DC-1 (Domain Controller) and the creation of Client-1

1. Create the Domain Controller VM (Windows Server 2022) named “DC-1”
   - Take note of the Resource Group and Virtual Network (Vnet) that was created at this time
2. Set Domain Controller’s NIC Private IP address to be static
3. Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created in Step 1.a
4. Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher

</p>
<br />

<p>

</p>
<p>







</p>
<br />

<p>
<img src="https://imgur.com/WTsRBS9.jpg" height="80%" width="80%" alt="Screenshot of the installation of Active Directory on DC-1"/>
</p>
<p>
Install Active Directory


8. Login to DC-1 and install Active Directory Domain Services
9. Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)
10. Restart and then log back into DC-1 as user: mydomain.com\labuser
</p>
<br />


<p>
<img src="https://imgur.com/61graiy.jpg" height="80%" width="80%" alt="Screenshot in AD of 2OU's EMPLOYEES & ADMINS and jane added to admins"/>
</p>
<p>
Create an Admin and Normal User Account in AD


11. In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
12. Create a new OU named “_ADMINS”
13. Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”
14. Add jane_admin to the “Domain Admins” Security Group
15. Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”
16. User jane_admin as your admin account from now on
</p>
<br />

<p>
<img src="https://imgur.com/20QPRC3.jpg" height="80%" width="80%" alt="Screenshot of jane_admin logged into Client-1 Client-1 is using DC-1 private IPaddress"/>
</p>
<p>
Join Client-1 to your domain (mydomain.com)


17. From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
18. From the Azure Portal, restart Client-1
19. Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)
20. Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in ADUC


</p>
<br />

<p>
<img src="https://imgur.com/JSp2R6F.jpg" height="80%" width="80%" alt="Provided remote desktop access to the domain users"/>
</p>
<p>
Setup Remote Desktop for non-administrative users on Client-1


22. Log into Client-1 as mydomain.com\jane_admin and open system properties
23. Click “Remote Desktop”
24. Allow “domain users” access to remote desktop
25. You can now log into Client-1 as a normal, non-administrative user now


</p>
<br />

<p>
<img src="https://imgur.com/6YuPBff.jpg" height="80%" width="80%" alt="Screenshot of employees added in AD"/>
</p>
<p>
Create a bunch of additional users and attempt to log into client-1 with one of the users


26. Login to DC-1 as jane_admin
27. Open PowerShell_ise as an administrator
28. Create a new File and paste the contents of the script into it (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)
29. Run the script and observe the accounts being created
30. When finished, open ADUC and observe the accounts in the appropriate OU
    - attempt to log into Client-1 with one of the accounts (take note of the password in the script)


Example of one of the added employees signed on to Client-1:

<img src="https://imgur.com/vdMMSFx.jpg" height="80%" width="80%" alt="Screenshot of employee bac.colok signed on in Client-1"/>
</p>
<br />
