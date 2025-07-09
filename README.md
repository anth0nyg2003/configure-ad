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

- Windows Server 2022 Datacenter
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Resource Group & Virtual Network
- Create Virtual Machine (Domain Controller)
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>
 <img src=https://github.com/user-attachments/assets/b997a664-34cc-4fce-9be2-57541b5fd675/>
 <img src=https://github.com/user-attachments/assets/23c3b5d6-6ae7-49cc-b617-3f3b841a7b26/>

</p>
<p>
In the Azure portal, create a Resource Group named Active-Directory-Lab, and a Virtual Network called Active-Directory-VNet in the East 2 region. Going straight to Review + Create is fine for both steps
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/f9280da4-9930-4be2-9207-ad19663a865a"/>
</p>
<p>
Create the VM DC-1 using the Windows Server 2022 Datacenter image with at least 2 vCPUs. Set the administrator username to labuser and the password to Cyberlab123!. Ensure that DC-1 is connected to the Active-Directory-VNet.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
