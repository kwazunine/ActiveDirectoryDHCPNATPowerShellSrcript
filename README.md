<h1>Active Directory PowerShell User Creation | DHCP | NAT</h1>

<h2>Description</h2>
This walkthrough covers deploying Active Directory in an on-premises environment, configuring Network Address Translation (NAT) and Dynamic Host Configuration Protocol (DHCP) for domain client computers to get connected to the internet, and utilizing a PowerShell script to create over 1000 users in Active Directory.
<br />


<h2>Technologies & Utilities Used</h2>

- <b>Active Directory</b>
- <b>DHCP</b>
- <b>Oracle VM VirtualBox</b>
- <b>PowerShell</b>
- <b>Routing and Remote Access</b> 

<h2>Operating Systems Used </h2>

- <b>Windows 10 Enterprise</b> (21H2)
- <b>Windows Server 2019</b>


<h2 align="center">Environment Map</h2>
<p align="center">
The Windows Server 2019 Domain Controller will have two network interface cards (NICs). One NIC (NAT) connects directly to the global internet, while the other NIC (Internal) connects to the internal virtual network. The domain will be jamrocknation.com, the internal IP address subnet will be 172.16.0.0/24, and the Domain Controller will provide DHCP, DNS, and NAT services for clients connected to the internal network.<br />
<img src="https://i.imgur.com/5NBo7w5.png" height="100%" width="100%" alt="Environment Map"/>
<br />
</p>

<h2 align="center">Network Adapters & Server Name Configuration</h2>
<p align="center">
Domain Controller Oracle VM VirtualBox Adapter Settings: <br/>
<img src="https://i.imgur.com/lk3QQ9P.png" height="80%" width="80%" alt="Domain Controller Oracle VM VirtualBox Adapter Settings"/>
<br />
<img src="https://i.imgur.com/2rMfJ6L.png" height="80%" width="80%" alt="Domain Controller Oracle VM VirtualBox Adapter Settings"/>
<br />
Renaming Domain Controller Windows Network Adapters:  <br/>
<img src="https://i.imgur.com/1icpK93.png" height="80%" width="80%" alt="Renaming Domain Controller Windows Network Adapters"/>
<br />
<img src="https://i.imgur.com/eAbEiXg.png" height="80%" width="80%" alt="Renaming Domain Controller Windows Network Adapters"/>
<br />
Domain Controller Windows Internal Network Adapter Settings: <br/>
<img src="https://i.imgur.com/wUdOh55.png" height="80%" width="80%" alt="Domain Controller Windows Internal Network Adapter Settings"/>
<br />
Naming The Server "DC":  <br/>
<img src="https://i.imgur.com/hZt8Ast.png" height="80%" width="80%" alt="Naming The Server "DC""/>
<br />
<br />
</p>
<h2 align="center">Setup & Configure Active Directory</h2>
<p align="center">
Setup Active Directory:  <br/>
<img src="https://i.imgur.com/m5rZLYn.png" height="80%" width="80%" alt="Setup Active Directory"/>
<br />
<img src="https://i.imgur.com/dalAdbJ.png" height="80%" width="80%" alt="Setup Active Directory"/>
<br />
<img src="https://i.imgur.com/u233j8R.png" height="80%" width="80%" alt="Setup Active Directory"/>
<br />
<img src="https://i.imgur.com/80TL8gk.png" height="80%" width="80%" alt="Setup Active Directory"/>
<br />
Configure Active Directory:  <br/>
<img src="https://i.imgur.com/In78fkJ.png" height="80%" width="80%" alt="Configure Active Directory"/>
<br />
<img src="https://i.imgur.com/Sn2HnQr.png" height="80%" width="80%" alt="Configure Active Directory"/>
<br />
<img src="https://i.imgur.com/2Z8FzMw.png" height="80%" width="80%" alt="Configure Active Directory"/>
<br />
<img src="https://i.imgur.com/s1NnPhI.png" height="80%" width="80%" alt="Configure Active Directory"/>
<br />
<img src="https://i.imgur.com/3W4uwgM.png" height="80%" width="80%" alt="Configure Active Directory"/>
<br />
Windows Login Screen To Sign Into Domain:  <br/>
<img src="https://i.imgur.com/0CTkAPc.png" height="80%" width="80%" alt="Windows Login Screen To Sign Into Domain"/>
</p>
<h2 align="center">Create Organizational Unit & Active Directory Administrator User</h2>
<p align="center">
Create Organizational Unit:  <br/>
<img src="https://i.imgur.com/AQztRkV.png" height="80%" width="80%" alt="Create Organizational Unit"/>
<br />
<img src="https://i.imgur.com/UY9vC6c.png" height="80%" width="80%" alt="Create Organizational Unit"/>
<br />
Create AD Admin User:  <br/>
<img src="https://i.imgur.com/vCD87N1.png" height="80%" width="80%" alt="Create AD Admin User"/>
<br />
<img src="https://i.imgur.com/b2gNln1.png" height="80%" width="80%" alt="Create AD Admin User">
<br />
<img src="https://i.imgur.com/HSPyVo5.png" height="80%" width="80%" alt="Create AD Admin User"/>
<br />
Add AD Admin User To Domain Admin Group:  <br/>
<img src="https://i.imgur.com/Hhe9AAE.png" height="80%" width="80%" alt="Add AD Admin User To Domain Admin Group"/>
<br />
<img src="https://i.imgur.com/qCCingZ.png" height="80%" width="80%" alt="Add AD Admin User To Domain Admin Group"/>
<br />
<img src="https://i.imgur.com/LKUm6v1.png" height="80%" width="80%" alt="Add AD Admin User To Domain Admin Group"/>
<br />
<img src="https://i.imgur.com/EUD3L9r.png" height="80%" width="80%" alt="Add AD Admin User To Domain Admin Group"/>
<br />
Sign In With AD Admin User:  <br/>
<img src="https://i.imgur.com/sSAYoSq.png" height="80%" width="80%" alt="Sign In With AD Admin User"/>
</p>
<h2 align="center">Setup & Configure Routing and Remote Acecss</h2> <br/>
<p align="center">
Setup Routing and Remote Acecss:  <br/>
<img src="https://i.imgur.com/hKDUxqQ.png" height="80%" width="80%" alt="Setup Routing and Remote Acecss"/>
<br />
<img src="https://i.imgur.com/yNVAXH4.png" height="80%" width="80%" alt="Setup Routing and Remote Acecss"/>
<br />
Configure Routing and Remote Acecss:  <br/>
<img src="https://i.imgur.com/a2iVXVX.png" height="80%" width="80%" alt="Configure Routing and Remote Acecss"/>
<br />
<img src="https://i.imgur.com/xFsrTQS.png" height="80%" width="80%" alt="Configure Routing and Remote Acecss"/>
<br />
<img src="https://i.imgur.com/EgscLJb.png" height="80%" width="80%" alt="Configure Routing and Remote Acecss"/>
<br />
<img src="https://i.imgur.com/lCUBa13.png" height="80%" width="80%" alt="Configure Routing and Remote Acecss"/>
<br />
</p>
<h2 align="center">Setup & Configure DHCP Server</h2> <br/>
<p align="center">
Setup DHCP Server:  <br/>
<img src="https://i.imgur.com/YUH8syg.png" height="80%" width="80%" alt="Setup DHCP Server"/>
<br />
Configure DHCP Server:  <br/>
<img src="https://i.imgur.com/seXTEwa.png" height="80%" width="80%" alt="Configure DHCP Server"/>
<br />
<img src="https://i.imgur.com/7CZRq8x.png" height="80%" width="80%" alt="Configure DHCP Server"/>
<br />
<img src="https://i.imgur.com/ym95xVQ.png" height="80%" width="80%" alt="Configure DHCP Server"/>
<br />
<img src="https://i.imgur.com/6fPPm86.png" height="80%" width="80%" alt="Configure DHCP Server"/>
<br />
<img src="https://i.imgur.com/M4ZWXBM.png" height="80%" width="80%" alt="Configure DHCP Server"/>
<br />
<img src="https://i.imgur.com/mR6VBvZ.png" height="80%" width="80%" alt="Configure DHCP Server"/>
<br />
<img src="https://i.imgur.com/1lMQFI7.png" height="80%" width="80%" alt="Configure DHCP Server"/>
<br />
<img src="https://i.imgur.com/97k8mgx.png" height="80%" width="80%" alt="Configure DHCP Server"/>
<br />
<img src="https://i.imgur.com/I6doKYH.png" height="80%" width="80%" alt="Configure DHCP Server"/>
<br />
</p>
<h2 align="center">Active Directory Organizational Unit & User Creation With PowerShell Script</h2> <br/>
<p align="center">
PowerShell Script Files:  <br/>
<img src="https://i.imgur.com/lsv7aD1.png" height="80%" width="80%" alt="PowerShell Script Files"/>
<br />
<img src="https://i.imgur.com/slwtMpH.png" height="80%" width="80%" alt="PowerShell Script Files"/>
<br />
<img src="https://i.imgur.com/wPR2E3F.png" height="80%" width="80%" alt="PowerShell Script Files"/>
<br />
Running PowerShell Script With Windows PowerShell ISE:  <br/>
<img src="https://i.imgur.com/SLegKFL.png" height="80%" width="80%" alt="Windows PowerShell ISE:"/>
<br />
<img src="https://i.imgur.com/Fc8ADLA.png" height="80%" width="80%" alt="Windows PowerShell ISE:"/>
<br />
<img src="https://i.imgur.com/1aq0vHx.png" height="80%" width="80%" alt="Windows PowerShell ISE:"/>
<br />
<img src="https://i.imgur.com/5gSGCtm.png" height="80%" width="80%" alt="Windows PowerShell ISE:"/>
<br />
PowerShell Script Results:  <br/>
<br />
<img src="https://i.imgur.com/v05aqVS.png" height="80%" width="80%" alt="PowerShell Script Results"/>
<br />
<img src="https://i.imgur.com/f800S1m.png" height="80%" width="80%" alt="PowerShell Script Results"/>
<br />
</p>
<h2 align="center">Joining Windows 10 Client Machine To Active Directory Domain</h2> <br/>
<p align="center">
<br />
Renaming Windows 10 Client Machine & Joining Windows 10 Client Machine To Active Directory Domain:  <br/>
<img src="https://i.imgur.com/10ghrQx.png" height="80%" width="80%" alt="PowerShell Script Files"/>
<br />
<img src="https://i.imgur.com/3XuHhV4.png" height="80%" width="80%" alt="PowerShell Script Files"/>
<br />
<img src="https://i.imgur.com/DU4v01l.png" height="80%" width="80%" alt="PowerShell Script Files"/>
<br />
Sign Into Windows 10 Client Machine With PowerShell Script Active Directory Created User  <br/>
<img src="https://i.imgur.com/u1Ew5H4.png" height="80%" width="80%" alt="Windows PowerShell ISE:"/>
<br />
<img src="https://i.imgur.com/ukECN6v.png" height="80%" width="80%" alt="Windows PowerShell ISE:"/>
<br />
<img src="https://i.imgur.com/AKS89Fl.png" height="80%" width="80%" alt="Windows PowerShell ISE:"/>
<br />
<img src="https://i.imgur.com/2933q2p.png" height="80%" width="80%" alt="Windows PowerShell ISE:"/>
<br />
</p>


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
