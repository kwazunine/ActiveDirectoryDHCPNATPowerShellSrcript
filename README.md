<h1>Active Directory | PowerShell User Creation</h1>

<h2>Description</h2>
This walkthrough covers deploying Active Directory on-premises, configuring a DHCP pool for client workstations, and utilizing a PowerShell script to create over 1000 users in Active Directory.
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
<img src="https://i.imgur.com/Z79cmTd.png" height="100%" width="100%" alt="Environment Map"/>
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

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
