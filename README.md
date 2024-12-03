<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022, 2vCPUs, 8GM RAM
- Windows 10 Pro (22H2), 2vCPUs, 8GB RAM

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1: Install Active Directory
- Step 2: Create a Domain Admin user for the domain
- Step 3: Join client-1 to domain

<h2>Deployment and Configuration Steps</h2>

<p>
Deploy two VMs in Azure within the same virtual network: a Windows Server (DC-1) for the domain controller and a Windows Pro (Client-1) for the client. Once deployed, log in to DC-1.
</p>
<br />
<p>
<img src="https://github.com/user-attachments/assets/ef543e6d-bb7b-4d64-a738-8154d99c527d" height="80%" width="80%" alt="server manager in DC-1"/>
</p>
<p>
Open Server Manager (it usually loads automatically, or you can find it in the Start menu). Click "Add roles and features," accept the defaults, and select "Active Directory Domain Services" in the "Select Server Roles" section.
</p>
<br />
<p>
<img src="https://github.com/user-attachments/assets/4ffa26fb-7ae8-49d9-842f-992d1a0f7f25" height="80%" width="80%" alt="installing AD"/>
</p>
<p>
Continue with this and check Restart the destination server automatically if required before clicking Install. After installation is complete, go back to the Server manager and click on the flagged icon in the top right. Then, click on the link that says to Promote this server to a domain controller. 
</p>
<br />
<p>
<img src="https://github.com/user-attachments/assets/39f7e7a9-02cc-472e-b830-ba39f105bd64" height="80%" width="80%" alt="promote to domain controller"/>
</p>
<p>
In the deployment configuration, choose "Add a new forest" and enter a domain name (e.g., "mydomain.com"). You can choose any valid domain name.
</p>
<br />
<p>
<img src="https://github.com/user-attachments/assets/3b52a9aa-44cc-4042-b7bf-e3742dccfbb0" height="80%" width="80%" alt="add new forest mydomain"/>
</p>
<p>
    Continue the Active Directory configuration:

You'll be prompted to set a Directory Services Restore Mode password. This password is rarely used, so any password will suffice.
Proceed with the remaining configuration steps. The server will restart to complete the Active Directory installation, and you'll be logged out.

    Verify client login:

    Log in to Client-1 using the format mydomain.com\(your username) and your password.

    Create a Domain Admin user on DC-1:

        Log back in to DC-1.
        Open the Start menu and navigate to Windows Administrative Tools > Active Directory Users and Computers.
        Right-click on mydomain.com in the left pane and select New > Organizational Unit (OU).
</p>
<br />
<p>
<img src="https://github.com/user-attachments/assets/faf44d3e-095c-46aa-8990-f9d396e694e4" height="80%" width="80%" alt="create OU for domain"/>
</p>
<p>
Create two OUs: "_EMPLOYEES" and "_ADMINS." Create an admin user named "Jane Doe" (username "jane_admin") within the "_ADMINS" OU and set a password. To grant domain admin privileges, right-click Jane Doe > Properties > Member Of, type "Domain Admins," click "Check Names," and apply the changes.
</p>
<br />
<p>
<img src="https://github.com/user-attachments/assets/09c0899a-a5c6-42b8-be70-83021c9dccc9" height="80%" width="80%" alt="set Jane as Domain admin"/>
</p>
<br />
Configure Client-1's network settings to use DC-1's private IP address as its DNS server.

<p>
<img src="https://github.com/user-attachments/assets/5bc33311-7037-4a64-ac19-6d11909e6ce2" height="80%" width="80%" alt="preconfigure vms before deploy AD"/>
</p>
<br />
<p>
Log back into Client-1 as Jane, be sure to do mydomain.com\ before the username. Right click on the Start menu -> Settings -> Rename this PC (advanced). Then under Computer Name click on Change and in Domain, type mydomain.com and OK.
</p>

<p>
<img src="https://github.com/user-attachments/assets/b847bdfa-2562-48b4-be8d-3fc4304810f1" height="80%" width="80%" alt="join client-1 to domain"/>
<img src="https://github.com/user-attachments/assets/af138c07-f43f-490c-bc8a-3199ba175601" height="80%" width="80%" alt="client joined domain"/>
</p>
<p>
Restart Client-1. On DC-1, verify Client-1 appears in Active Directory Users and Computers > mydomain.com > Computers.
</p>
<br />

<p>
  <img src="https://github.com/user-attachments/assets/1344ee78-88e2-49e9-8496-933bd354572d" height="80%" width="80%" alt="confirm client 1 in domain"/>
</p>
<p>

</p>
