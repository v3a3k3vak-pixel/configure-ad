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


<h2>Deployment and Configuration Steps</h2>

<p>
</p>
<p>
In this lab, we'll create two VMs in the same VNet: a Domain Controller and a client machine. We'll assign the Domain Controller a static IP, configure the client's DNS settings to point to the Domain Controller, and join the client to the domain.
</p>
<br />

<p>
<img width="506" height="410" alt="Screenshot 2026-10-26 074619" src="https://github.com/user-attachments/assets/03620582-9623-4d5d-958a-b3bdf55e1eee" />

</p>
First, assign DC-1 a static private IP address. Next, enable ICMPv4 in DC-1's firewall to allow ping requests. From Client-1, ping DC-1 to verify network connectivity. A successful ping confirms that both VMs can communicate.
<br />

<p>

</p>
<img width="1031" height="732" alt="Screenshot 2026-10-29 002814" src="https://github.com/user-attachments/assets/859fc9de-79f9-496e-a62c-5ed2a217373c" />

Next, log back into DC-1 and install Active Directory Users and Computers. Promote DC-1 to a Domain Controller and create a new forest named mydomain.com. Restart the VM, then sign back in using "mydomain.com\labuser". Once complete, open Active Directory Users and Computers to verify the installation.
<img width="995" height="708" alt="Screenshot 2026-10-31 145942" src="https://github.com/user-attachments/assets/354866c2-7806-4b4f-89af-2bd63a3ea5db" />

<br />
</p>
Next, create two Organizational Units (OUs) named _EMPLOYEES and _ADMINS. Right-click the domain, select New > Organizational Unit, and enter each name. Inside the _ADMINS OU, create a user named Jane Doe with the username "Jane_admin". Finally, add Jane_admin to the Domain Admins security group.
</p>
<img width="1046" height="732" alt="Screenshot 2026-10-31 151346" src="https://github.com/user-attachments/assets/8c5b210f-ed37-4141-958a-d2eda32924cf" />

<br />
</p>
<img width="1038" height="731" alt="Screenshot 2026-10-31 151523" src="https://github.com/user-attachments/assets/55a7a31e-c4d6-4fb2-ba56-871befb61828" />

From this point forward, use "Jane_admin" as the administrator account. Next, configure Client-1's DNS settings in the Azure portal to use DC-1's private IP address. Restart Client-1, then verify that it is using DC-1 as its DNS server.
</p>
<img width="1535" height="805" alt="Screenshot 2026-10-31 155722" src="https://github.com/user-attachments/assets/dcd68a99-8704-4223-897b-5595d36af8d5" />

<br />
</p>
<img width="1032" height="737" alt="image" src="https://github.com/user-attachments/assets/5471a8ff-89be-4be5-b7d3-a92195182258" />

</p>
<p>
</p>
<p>
Next, join Client-1 to the domain. Open System Settings > About > Rename this PC (Advanced), then select Change and enter "mydomain.com". When prompted, enter your domain credentials ("mydomain.com\labuser"). Restart Client-1 to complete the domain join
</p>
<br />
<p>
  <p>
<img width="1033" height="742" alt="image" src="https://github.com/user-attachments/assets/7318cd29-3374-4d99-830b-e3d86aa2e293" />

</p>
Next, log into Client-1 as an administrator and open System Properties. Under Remote Desktop, add Domain Users to the list of users allowed to connect remotely. Once configured, standard domain users can log into Client-1 using Remote Desktop.
<br />

<p>
  <p>
<img width="892" height="751" alt="Screenshot 2026-11-01 064621" src="https://github.com/user-attachments/assets/7cb9884a-c88a-485d-ae77-db097e711812" />

</p>
<p>
Lastly to verify that normal users can RDP into Client-1 we will use a script to generate thousands of users into the domain. We will input the script in powershell, after the users are created we will select one and RDP into Client-1.
</p>
<br />
<img width="1048" height="745" alt="Screenshot 2026-11-01 070340" src="https://github.com/user-attachments/assets/a43d6df0-6826-4c1a-96e8-07560703f79d" />

<p>
<p>
  <p>
<img width="752" height="537" alt="Screenshot 2026-11-01 070835" src="https://github.com/user-attachments/assets/8a8adc7b-4649-425a-bafc-571557224c92" />


As you can see the Powershell script created a user with the username "bala.kav" We were able to login to Client-1 with his credentials as a normal user. 
</p>
