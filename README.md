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
- Windows 10 Pro (22H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Resource Group & Virtual Network
- Create Virtual Machines (Domain Controller & Client 1)
- Set Static IP for the Domain Controller
- Log in to Domain Controller via Remote Desktop and Disable Windows Firewall
- Configure Client-1 to Use DC-1 as its DNS server
- Verify Connectivity Between Client-1 and DC-1
- Install Active Directory Domain Services

<h2>Deployment and Configuration Steps</h2>

<p>
 <img src=https://github.com/user-attachments/assets/b997a664-34cc-4fce-9be2-57541b5fd675/>
 <img src=https://github.com/user-attachments/assets/23c3b5d6-6ae7-49cc-b617-3f3b841a7b26/>

</p>
<p>
In the Azure portal, create a Resource Group named Active-Directory-Lab, and a Virtual Network called Active-Directory-VNet in the East 2 region. Going straight to Review + Create is fine for both steps.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/f9280da4-9930-4be2-9207-ad19663a865a"/>
<img src="https://github.com/user-attachments/assets/d35b3308-f9e3-40a3-a9b1-8b0f7921b3ec"/>

</p>
<p>
Create the VM DC-1 using the Windows Server 2022 Datacenter image with at least 2 vCPUs. Set the administrator username to labuser and the password to Cyberlab123!. Ensure that DC-1 is connected to the Active-Directory-VNet. After Review + Create then Create.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/41f5e412-44e7-4b00-9be6-ce1d24b9fb0c"/>
<img src="https://github.com/user-attachments/assets/44ca1b34-67f3-4fab-9ecd-83818adaabcd"/>

</p>
<p>
Create the VM Client-1using the Windows 10 Pro image. Use the same credentials as for DC-1 and connect Client-1 to the Active-Directory-VNet. Then Review + Create, and Create.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/d63f75ae-24d7-40fb-82d6-fc0e9929713c"/>
<img src="https://github.com/user-attachments/assets/b7fdf84d-c63c-45e0-bf04-894876f24e56"/>

</p>
<p>
Configure DC-1's network interface to use a static private IP address. You do this by going to network settings under networking of the dc-1 virtual machine. This step is crucial because the client will use this IP as its DNS server.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/9ce98f2c-2e4e-4ac9-8b57-c2bef90ae851"/>
<img src="https://github.com/user-attachments/assets/168044ad-e772-48b6-8166-75a6b0107107"/>

</p>
<p>
Remote into DC-1 using its Public IP via Remote Desktop. Log in using the credentials we set up above.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/463d7708-5e4c-4522-8632-cb0f24b96d5d"/>
<p>
This is what the remote desktop session looks like on DC-1.
</p>
<p>
<img src="https://github.com/user-attachments/assets/cc199de1-0369-4a4d-94a3-5f850a6ab6e1"/>
<img src="https://github.com/user-attachments/assets/5961ab1b-9d0a-4e3b-9868-9fc7cca1e4e4"/>
</p>
<p>
Right Click Start menu or the bottom left windows icon and click run. Type wf.msc for Windows Firewall.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/7b52e8ec-fb2d-4c5f-a1cf-76039b73e98e"/>
<img src="https://github.com/user-attachments/assets/4af3c22f-4b14-4019-8f81-d1d7847322c1"/>

</p>
<p>
In the Azure portal, navigate to DC-1 then Networking and copy the Domain Controller’s Private IP (in my case 10.0.0.4). Go to Client-1 > Networking and select its network interface configuration. Change the DNS Servers setting from Inherit from virtual network to Custom. Enter DC-1's Private IP as the DNS server and save the changes. Restart Client-1 to apply the new DNS settings.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/0b67fd44-1095-4853-a12c-e859f39fe77f"/>
<img src="https://github.com/user-attachments/assets/b8e73753-f69c-44ec-8c69-5b78b7ba1482"/>
<img src="https://github.com/user-attachments/assets/e63a8ebb-171f-4a2e-9b59-f58fca44f428"/>
</p>
<p>
Remote into Client-1 via its Public IP. Log in with the credentials above. You can select no for all the privacy settings and click accept.
<br />

<p>
<img src="https://github.com/user-attachments/assets/e3c03fb4-1c83-4f28-82fd-3a1626c035b6"/>
<img src="https://github.com/user-attachments/assets/575c0993-f623-4e40-af54-0c77555b6807"/>
<img src="https://github.com/user-attachments/assets/1c8321b0-3ab7-4a74-bbc1-e6863351fc24"/>

</p>
<p>
Open Windows PowerShell as Administrator. Run ping 10.0.0.4 (or the actual static IP of DC-1) to test connectivity. Run ipconfig /all to confirm that the DNS server for Client-1 is set to DC-1's Private IP. After that you can close client-1 as we need to remote in DC-1 for the next step.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/e72392df-829e-479d-b435-b64d215cdf5d"/>
<img src="https://github.com/user-attachments/assets/c87f18d5-fb30-49de-9703-35d89d1a0f6a"/>
<img src="https://github.com/user-attachments/assets/b5614164-101b-420a-b7f2-d699001e9d3a"/>
</p>
<p>
Remote into DC-1 via its Public IP. Log in with the credentials above. Once logged in, click on start (bottom left Windows Icon) and click on Server Manager. Click Add Roles and Features. Select Active Directory Domain Services from the list and complete the wizard. Add features and click next to all steps. Check "Restart the destination server automatically if required." Allow the system to restart after installation.
<br />

<p>
<img src="https://github.com/user-attachments/assets/9627c055-c4b8-4a85-bb07-396c468f29f6"/>
<img src="https://github.com/user-attachments/assets/518e0249-c342-40d8-9f3f-afd4a177689c"/>
<img src="https://github.com/user-attachments/assets/d1108b91-efdf-4584-90e3-11756dc1bf80"/>
<img src="https://github.com/user-attachments/assets/99f8c575-6fb8-452a-b084-ce4adaf66ced"/>
</p>
<p>
After the restart, in Server Manager click the flag icon and select Promote this server to a domain controller. Choose Add a new forest and enter mydomain.com as the root domain name. Provide the Directory Services Restore Mode (DSRM) password (Password1) and complete the wizard. The system will restart; upon logging back in, your login should display mydomain.com\labuser.
<br />

<p>
<img src="https://github.com/user-attachments/assets/bb7fd9f9-e91b-4fe6-8c98-0c019c5c1e2d"/>
<img src="https://github.com/user-attachments/assets/e14cd81c-b1fe-44a2-9c62-59dad229ff7e"/>
<img src="https://github.com/user-attachments/assets/26be7822-10cd-4326-b909-605b68293078"/>
</p>
<p>
On DC-1, open Active Directory Users and Computers (ADUC). Create two Organizational Units (OUs) under mydomain.com (e.g., _EMPLOYEES and _ADMINS). Create a new user (e.g., Jane Doe with logon name jane_admin@mydomain.com and password Cyberlab123!) and add the user to the Domain Admins group.
<br />

<p>
<img src="https://github.com/user-attachments/assets/bb7fd9f9-e91b-4fe6-8c98-0c019c5c1e2d"/>
<img src="https://github.com/user-attachments/assets/e14cd81c-b1fe-44a2-9c62-59dad229ff7e"/>
<img src="https://github.com/user-attachments/assets/26be7822-10cd-4326-b909-605b68293078"/>
</p>
<p>
Remote Desktop into Client-1 using it's public IP address.
<br />
