<h1>Active Directory | DHCP | NAT | PowerShell Script 'User Creation'</h1>

<h2>Description</h2>
This walkthrough covers deploying Active Directory in an on-premises environment, configuring Network Address Translation (NAT) and Dynamic Host Configuration Protocol (DHCP) for clients to get connected to the internet, and utilizing a PowerShell script to create over 1000 users in Active Directory.
<br />

<h2>Technologies & Utilities Used</h2>

- <b>Active Directory</b>
- <b>DHCP</b>
- <b>Oracle VM VirtualBox</b> (Virtual Machines (VM))
- <b>Windows PowerShell ISE</b>
- <b>Routing and Remote Access</b> 

<h2>Operating Systems Used</h2>

- <b>Windows 10 Enterprise</b> (21H2)
- <b>Windows Server 2019</b>

<h2>Prerequisites</h2>

- <b>Default Configured Windows 10 Enterprise VM</b>
- <b>Default Configured Windows Server 2019 VM</b>

<h2>Environment Map & Overview</h2>
<img src="https://i.imgur.com/5NBo7w5.png" height="100%" width="100%" alt="Environment Map"/>
The Windows Server 2019 Domain Controller will have two network interface cards (NICs). One NIC (NAT) connects to the global internet, while the other NIC (Internal) connects to the internal virtual network. The domain will be 'jamrocknation.com', the internal virtual network IP address subnet will be '172.16.0.0/24', and the Domain Controller will provide DHCP, DNS, and NAT services for clients connected to the internal virtual network. <br />
<br />

<h2 align="center">Network Adapters and Server Name Configuration</h2>

<h3 align="center">Windows Server 2019 Oracle VM VirtualBox Adapter Settings:</h3>
<p align="center">
Before configuring the Windows Server 2019 VM, ensure that the VM in Oracle VM VirtualBox has two network adapters enabled in its settings, as depicted in the images below.<br/>
<img src="https://i.imgur.com/lk3QQ9P.png" height="80%" width="80%" alt="Domain Controller Oracle VM VirtualBox Adapter Settings"/>
<br />
<img src="https://i.imgur.com/2rMfJ6L.png" height="80%" width="80%" alt="Domain Controller Oracle VM VirtualBox Adapter Settings"/>
<br />
</p>

<h3 align="center">Renaming the Windows Server 2019 Network Adapters:</h3>
<p align="center">
Once logged into the Windows Server 2019 VM, both network adapters should be renamed via the Windows Control Panel's Network Connections. This will help in identifying the correct network adapter when configuring NAT with the Routing and Remote Access service. <br/>
1. Right-click each network adapter and select 'Rename'. <br/>
<img src="https://i.imgur.com/1icpK93.png" height="80%" width="80%" alt="Renaming Domain Controller Windows Network Adapters"/>
<br />
2. Rename the 'Ethernet' network adapter to 'NAT,' as it will function as the NAT NIC. Rename the 'Ethernet 2' network adapter to 'Internal,' as it will connect to the internal virtual network. <br/>
<img src="https://i.imgur.com/eAbEiXg.png" height="80%" width="80%" alt="Renaming Domain Controller Windows Network Adapters"/>
<br />
</p>

<h3 align="center">Windows Server 2019 Internal Network Adapter Settings:</h3>
<p align="center">
3. Right-click the 'Internal' network adapter, then choose Properties > Internet Protocol Version 4 (TCP/IPv4). Enter the following information into the Internet Protocol Version 4 (TCP/IPv4) properties fields: <br/>
'172.16.0.1' for the IP address. <br/>
'255.255.255.0' for the Subnet mask. <br/>
'127.0.0.1' for Preferred DNS server as the Domain Controller will provide DNS services. <br/>
Click 'OK' when finished. <br />
<img src="https://i.imgur.com/wUdOh55.png" height="80%" width="80%" alt="Domain Controller Windows Internal Network Adapter Settings"/>
<br />
</p>

<h3 align="center">Naming the Server:</h3>
<p align="center">
4. Launch 'System Properties' via Settings>System>About>Advanced System Settings to rename the server to 'DC'. Click the 'Computer Name' tab, then select 'Change'. Enter 'DC' in the 'Computer name' field, then click 'OK'. Restart the server when prompted. <br />
<img src="https://i.imgur.com/hZt8Ast.png" height="80%" width="80%" alt="Naming The Server "DC""/>
<br />
</p>

<h2 align="center">Setup & Configure Active Directory</h2>

<h3 align="center">Setup Active Directory:</h3>
<p align="center">
1. Open 'Server Manager' if it did not launch automatically after the server restart. Then, select the 'Manage' menu in the top right and choose 'Add Roles and Features'. <br/>
<img src="https://i.imgur.com/m5rZLYn.png" height="80%" width="80%" alt="Setup Active Directory"/>
<br />
2. Proceed by clicking 'Next' until the 'Server Selection' window appears, as shown below. Verify that 'DC' is highlighted and click 'Next'. <br/>
<img src="https://i.imgur.com/dalAdbJ.png" height="80%" width="80%" alt="Setup Active Directory"/>
<br />
3. Choose the 'Active Directory Domain Services" role and click 'Add Features'. <br/>
<img src="https://i.imgur.com/u233j8R.png" height="80%" width="80%" alt="Setup Active Directory"/>
<br />
4. Continue clicking the 'Next' and 'Install' buttons as prompted until the installation succeeds. After the installation succeeds message appears, click 'Close' to close the window. <br/>
<img src="https://i.imgur.com/80TL8gk.png" height="80%" width="80%" alt="Setup Active Directory"/>
<br />
</p>

<h3 align="center">Configure Active Directory:</h3>
<p align="center">
5. To configure the Active Directory Domain Controller, click the alert menu icon with the yellow triangle exclamation in the top right of Server Manager, then select 'Promote this server to a domain controller' in the drop down menu. <br/>
<img src="https://i.imgur.com/In78fkJ.png" height="80%" width="80%" alt="Configure Active Directory"/>
<br />
6. Enter the domain 'jamrocknation.com'(any domain name can be used) into the 'Root domain name' field as shown below, then click 'Next'.  <br/>
<img src="https://i.imgur.com/Sn2HnQr.png" height="80%" width="80%" alt="Configure Active Directory"/>
<br />
7. Create a 'Directory Services Restore Mode' password, then proceed by clicking 'Next' until the 'Install' button is no longer greyed out. <br/>
<img src="https://i.imgur.com/2Z8FzMw.png" height="80%" width="80%" alt="Configure Active Directory"/>
<br />
8. Click the 'Install' button to let the process begin. Once the server is configured, a prompt stating the server is being restarted because Active Directory was installed will appear. Select 'Close' on the prompt to let the server restart.
<img src="https://i.imgur.com/3W4uwgM.png" height="80%" width="80%" alt="Configure Active Directory"/>
<br />
</p>

<h3 align="center">Windows Login Screen to Login to the Domain:</h3>
<p align="center">
9. After the server restarts, the login screen should appear as depicted in the image below. It will display the option to sign into the newly configured Active Directory Domain Controller. Proceed to log in to the Domain Controller. <br/>
<img src="https://i.imgur.com/0CTkAPc.png" height="80%" width="80%" alt="Windows Login Screen To Sign Into Domain"/>
<br />
</p>

<h2 align="center">Create Organizational Unit and Active Directory Administrator User</h2>

<h3 align="center">Create Organizational Unit:</h3>
<p align="center">
Now that Active Directory is configured and deployed, the next step is to create an Organizational Unit for Domain administrator user accounts. <br/>
1. Launch 'Active Directory Users and Computers'. Right-click the domain name in the left sidebar, then select 'New' > 'Organizational Unit' as demonstrated in the image below. <br/>
<img src="https://i.imgur.com/AQztRkV.png" height="80%" width="80%" alt="Create Organizational Unit"/>
<br />
2. Name the Organizational Unit following the format shown in the image below, then click the 'OK' button when finished. <br/>
<img src="https://i.imgur.com/UY9vC6c.png" height="80%" width="80%" alt="Create Organizational Unit"/>
<br />
</p>

<h3 align="center">Create Active Directory Admin User:</h3>
<p align="center">
The next step is to create an Active Directory user with 'Domain Admin' privileges in the newly created Organizational Unit. Having an Active Directory user with Domain Admin rights will simplify configuring the remaining services and executing the PowerShell script to create over 1000 Active Directory user accounts.  <br/>
3. Select the Organzational Unit that was just created from the left sidebar. Right-click the white space on the right side in the Organizational Unit folder, then select 'New' > 'User' as shown in the image below. <br/>  
<img src="https://i.imgur.com/vCD87N1.png" height="80%" width="80%" alt="Create AD Admin User"/>
<br />
4. Fill out the name and user logon name fields following the format shown in the image below. Click 'Next' to set the password, ensure the 'User must change password at next logon' checkbox is unchecked, and then click 'Next' > 'Finish' to complete the user creation. <br/>
<img src="https://i.imgur.com/b2gNln1.png" height="80%" width="80%" alt="Create AD Admin User">
<br />
5. The newly created user now appears in the Organizational Unit folder on the right side.  <br/>
<img src="https://i.imgur.com/HSPyVo5.png" height="80%" width="80%" alt="Create AD Admin User"/>
<br />
</p>

<h3 align="center">Add Active Directory Admin User to Domain Admin Group:</h3>
<p align="center">
With the user created, the user now needs to be added to the 'Domain Admins' security group to grant Domain Admin privileges. <br/>
6. Right-click the user on the right side in the Organizational Unit folder, then select 'Properties' as depicted in the image below. <br/>
<img src="https://i.imgur.com/Hhe9AAE.png" height="80%" width="80%" alt="Add AD Admin User To Domain Admin Group"/>
<br/>
7. Select the 'Member Of' tab in the user properties window, then click the 'Add' button. <br/> 
<img src="https://i.imgur.com/qCCingZ.png" height="80%" width="80%" alt="Add AD Admin User To Domain Admin Group"/>
<br />
8. Enter 'Domain Admins' in the 'Enter the object names to select' field, click the 'Check Names' button to validate, and then click 'OK'. <br/> 
<img src="https://i.imgur.com/LKUm6v1.png" height="80%" width="80%" alt="Add AD Admin User To Domain Admin Group"/>
<br />
9. 'Domain Admins' should now appear under the 'Member Of' tab in the user properties window. Close the user properties window and Active Directory Users and Computers. Finally, sign out of the Domain Controller. <br />
<img src="https://i.imgur.com/EUD3L9r.png" height="80%" width="80%" alt="Add AD Admin User To Domain Admin Group"/>
<br />
</p>

<h3 align="center">Sign in with Active Directory Admin User:</h3>
<p align="center">
10. Sign in to the Domain Controller with the newly created Domain Admin user. <br/>
<img src="https://i.imgur.com/sSAYoSq.png" height="80%" width="80%" alt="Sign In With AD Admin User"/>
<br />
</p>

<h2 align="center">Setup and Configure Routing and Remote Access</h2>

<h3 align="center">Setup Routing and Remote Acecss:</h3>
<p align="center">
The 'Routing and Remote Access' service will perform NAT for clients connected to the internal virtual network, facilitating connectivity to the global internet. Adding the 'Remote Access' server role to the Domain Controller via Server Manager follows a process similar to what was done with Active Directory Domain Services earlier.<br/>
1. Launch the 'Add Roles and Features Wizard', and continue clicking the 'Next' button until you reach the 'Server Roles' window. Then, select Remote Access and proceed by clicking 'Next' until the 'Add Features' button appears, then click it. <br/> 
<img src="https://i.imgur.com/hKDUxqQ.png" height="80%" width="80%" alt="Setup Routing and Remote Access"/>
<br />
2. Verify that both the 'DirectAccess and VPN (RAS)' and 'Routing' services checkboxes are checked on the 'Role Services' window. To complete the process, click the 'Next' and 'Install' buttons when prompted. Close the 'Add Roles and Features Wizard' when the installation succeeded message appears on the 'Results' window. <br/>  
<img src="https://i.imgur.com/yNVAXH4.png" height="80%" width="80%" alt="Setup Routing and Remote Access"/>
<br />
</p>

<h3 align="center">Configure Routing and Remote Access:</h3>
<p align="center">
3. Click the 'Tools' menu in the top right of Server Manager, then select 'Routing and Remote Access' When launched, right-click 'DC (local)' in the left sidebar and select 'Configure and Enable Routing and Remote Access' from the menu. <br/>
<img src="https://i.imgur.com/a2iVXVX.png" height="80%" width="80%" alt="Configure Routing and Remote Access"/>
<br />
4. Select the 'Next' button in the setup wizard to proceed to the 'Configuration' window. On this window choose the 'Network address translation (NAT)' option and click 'Next'. <br/>
<img src="https://i.imgur.com/xFsrTQS.png" height="80%" width="80%" alt="Configure Routing and Remote Access"/>
<br />
5. Choose the NAT network interface, which is the internet-facing NIC that will translate the IP addresses of client machines on the internal virtual network and enable internet connectivity for them. Select 'Next' and then click 'Finish' in the setup wizard to complete the process. <br/>
<img src="https://i.imgur.com/EgscLJb.png" height="80%" width="80%" alt="Configure Routing and Remote Access"/>
<br />
6. Routing and Remote Access should now display a green up arrow on the 'DC (local)' icon in the left sidebar, indicating a successful configuration. If the green up arrow is not shown, restart the Domain Controller. <br/>
<img src="https://i.imgur.com/lCUBa13.png" height="80%" width="80%" alt="Configure Routing and Remote Access"/>
<br />
</p>

<h2 align="center">Setup & Configure DHCP Server</h2>

<h3 align="center">Setup DHCP Server:</h3>
<p align="center">
The DHCP Server will automatically assign IP addresses to client machines on the internal virtual network from a range of IP addresses defined in the DHCP pool. <br/>
1. Open the Add Roles and Features Wizard again and proceed to the Server Roles window. No additional options are required to be selected, so select 'DHCP Server' and proceed through the prompts to add and install the DHCP Server features. Close the Add Roles and Features Wizard once the installation is complete. <br/>
<img src="https://i.imgur.com/YUH8syg.png" height="80%" width="80%" alt="Setup DHCP Server"/>
<br />
</p>

<h3 align="center">Configure DHCP Server:</h3>
<p align="center">
2. Access 'DHCP' from the Tools menu in Server Manager. <br/>
<img src="https://i.imgur.com/seXTEwa.png" height="80%" width="80%" alt="Configure DHCP Server"/>
<br />
3. Right-click 'IPv4' in the left sidebar and select 'New Scope' from the menu. <br/>
<img src="https://i.imgur.com/7CZRq8x.png" height="80%" width="80%" alt="Configure DHCP Server"/>
<br />
4. Click 'Next' in the setup wizard to proceed to the 'Scope Name' window. Enter '172.16.0.100-254' in the 'Name' field. This range represents the usable IP addresses that will be available to clients via DHCP on the internal virtual network's 172.16.0.0/24 subnet. <br/>
<img src="https://i.imgur.com/ym95xVQ.png" height="80%" width="80%" alt="Configure DHCP Server"/>
<br />
5. Continue to the 'IP Address Range' window by clicking 'Next' in the wizard. Enter '172.16.0.100' in the 'Start IP Address' field, '172.16.0.254' in the 'End IP Address' field, '24' in the 'Length' field, and '255.255.255.0' in the 'Subnet mask' field. <br/>
<img src="https://i.imgur.com/6fPPm86.png" height="80%" width="80%" alt="Configure DHCP Server"/>
<br />
6. Proceed to click the upcoming 'Next' buttons to get to the 'Router (Default Gateway)' window. '172.16.0.1' should be added in as the default gateway IP address as shown below in the image below. Select 'Next' after. <br/>
<img src="https://i.imgur.com/M4ZWXBM.png" height="80%" width="80%" alt="Configure DHCP Server"/>
<br />
7. On the 'Domain Name and DNS Servers' window, the 'Parent domain' and 'IP address' fields should populate with the information from the Domain Controller, which is 'jamrocknation.com' and '172.16.0.1' in this case. Complete the remaining wizard steps by proceeding to click the upcoming 'Next' and 'Finish' buttons when prompted. <br/>
<img src="https://i.imgur.com/mR6VBvZ.png" height="80%" width="80%" alt="Configure DHCP Server"/>
<br />
8. Now that the DHCP scope for the internal network clients is set, the Domain Controller must be authorized by right-clicking the Domain Controller 'dc.jamrocknation.com' in the right sidebar and selecting 'Authorize'. <br/>
<img src="https://i.imgur.com/1lMQFI7.png" height="80%" width="80%" alt="Configure DHCP Server"/>
<br />
9. Right-click the Domain Controller 'dc.jamrocknation.com' in the right sidebar again, then click 'Refresh'. <br/>
<img src="https://i.imgur.com/97k8mgx.png" height="80%" width="80%" alt="Configure DHCP Server"/>
<br />
10. A green checkmark should now appear on the 'IPv4' server icon in the left sidebar, and the DHCP scope address pool should appear when 'IPv4' is expanded in the left sidebar, as depicted in the image below. <br/>
<img src="https://i.imgur.com/I6doKYH.png" height="80%" width="80%" alt="Configure DHCP Server"/>
<br />
</p>
 
<h2 align="center">Active Directory Organizational Unit & User Creation With PowerShell Script</h2>

<h3 align="center">PowerShell Script Files:</h3>
<p align="center">
Creating a large number of Active Directory users is repetitive and time-consuming. Automating and simplifying this process can be achieved by utilizing a PowerShell script. <br/>
1. As shown in the image below, the PowerShell script named '1_CREATE_USERS' will source the names of 1000+ users from the 'names' text file. <br/>
<img src="https://i.imgur.com/lsv7aD1.png" height="80%" width="80%" alt="PowerShell Script Files"/>
<br />
2. The 'names' text file contains the first and last name of the users. <br/>
<img src="https://i.imgur.com/slwtMpH.png" height="80%" width="80%" alt="PowerShell Script Files"/>
<br />
3. Examining the PowerShell script below, the code shows that a password 'Change2YourOwn!' will be set for all users, a new Active Directory Organizational Unit 'JamRockNationUsers' will be created, and the users will be added to the 'JamRockNationUsers' Organizational Unit. <br/>
<a href="https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1">PowerShell Script Code Source</a> <br/>
<img src="https://i.imgur.com/wPR2E3F.png" height="80%" width="80%" alt="PowerShell Script Files"/>
<br />
</p>

<h3 align="center">Running PowerShell Script with Windows PowerShell ISE:</h3>
<p align="center">
4. Launch 'Windows PowerShell ISE' as an administrator, open the '1_CREATE_USERS' script in Windows PowerShell ISE, and navigate to the '1_CREATE_USERS' folder location using the Windows PowerShell ISE command line, as illustrated in the image below. <br/>
<img src="https://i.imgur.com/SLegKFL.png" height="80%" width="80%" alt="Windows PowerShell ISE:"/>
<br />
5. Enter the 'Set-ExecutionPolicy Unrestricted' cmdlet in the Windows PowerShell ISE command line to enable the ability to run the script. <br/>
<img src="https://i.imgur.com/Fc8ADLA.png" height="80%" width="80%" alt="Windows PowerShell ISE:"/>
<br />
6. Next, press the green triangle 'Run' button in the Windows PowerShell ISE menu at the top to execute the script. The Windows PowerShell ISE command line should then begin displaying the user accounts being created. <br/> 
<img src="https://i.imgur.com/1aq0vHx.png" height="80%" width="80%" alt="Windows PowerShell ISE:"/>
<br />
7. Once the script finishes running, 'Completed' should appear in the lower left corner of the Windows PowerShell ISE window. <br/> 
<img src="https://i.imgur.com/5gSGCtm.png" height="80%" width="80%" alt="Windows PowerShell ISE:"/>
<br />
</p>

<h3 align="center">PowerShell Script Results:</h3>
<p align="center">
8. Now lets verify the results of the PowerShell script. Open Active Directory Users and Computers where the 'JamRockNationUsers' Organizational Unit should now appear in the left sidebar under the domain 'jamrocknation.com'. As shown below, it does! <br/>  
<img src="https://i.imgur.com/v05aqVS.png" height="80%" width="80%" alt="PowerShell Script Results"/>
<br />
9. Right-clicking the domain 'jamrocknation.com' in the left sidebar and selecting 'Find' launches the 'Find Users, Contacts, and Groups' window. Observing the lower left of the window shows that 1053 items have been found, indicating that there are now 1000+ Active Directory users. <br/>
<img src="https://i.imgur.com/f800S1m.png" height="80%" width="80%" alt="PowerShell Script Results"/>
<br />
</p>

<h2 align="center">Joining Windows 10 Client Machine To Active Directory Domain</h2>

<h3 align="center">Renaming Windows 10 Client Machine and Joining Active Directory Domain Controller:</h3>
<p align="center">
With Active Directory deployed, DHCP and Routing and Remote Access services running on the Domain Controller, and over 1000 users created with a PowerShell script, joining a newly deployed Windows 10 Enterprise VM client to the Domain Controller will facilitate validation that everything is working as expected. <br/>
1. After logging into the Windows 10 client, open 'System Properties', navigate to the 'Computer Name' tab, and click the 'Change' button. In the 'Computer Name/Domain Changes' window, enter 'WS1' in the 'Computer name:' field, select the 'Domain' radio button, enter the domain name 'jamrocknation.com' in the 'Domain:' field, and click 'OK'. <br/>
<img src="https://i.imgur.com/10ghrQx.png" height="80%" width="80%" alt="Windows 10 Client Rename & Joining Active Directory Domain"/>
<br />
2. Enter the Active Directory administrator username and password into the 'Windows Security' prompt, as shown in the image below, then click the 'OK' button. <br/>
<img src="https://i.imgur.com/3XuHhV4.png" height="80%" width="80%" alt="Windows 10 Client Rename & Joining Active Directory Domain"/>
<br />
3. Click 'OK' on the 'Welcome to the domain' message. Next, restart the Windows 10 client. <br/>
<img src="https://i.imgur.com/DU4v01l.png" height="80%" width="80%" alt="Windows 10 Client Rename & Joining Active Directory Domain"/>
<br />
</p>

<h3 align="center">Sign into Windows 10 Client Machine with PowerShell Script Active Directory Created User</h3>
<p align="center">
4. At the Windows 10 client login screen, log in with one of the Active Directory users created by the PowerShell script. <br/>
<img src="https://i.imgur.com/u1Ew5H4.png" height="80%" width="80%" alt="Windows 10 Client Login Screen To Sign Into Domain"/>
<br />
5. Launch a 'Command Prompt' window on the Windows 10 client and enter 'whoami' to verify the Active Directory user logged in. Next, execute 'ipconfig' to confirm assignment of an IP address '172.16.0.100' from the DHCP service on the Domain Controller. Afterward, enter 'ping 8.8.8.8' to verify internet connectivity to the global internet, checking the echo replies from Google DNS servers confirms a successful connection! <br/>
<img src="https://i.imgur.com/ukECN6v.png" height="80%" width="80%" alt="Verifying AD User DHCP Internet Connectivity"/>
<br />
6. To continue validation, launch Active Directory Users and Computers on the Domain Controller. Select 'Computers' from the left sidebar, where the Windows 10 client 'WS1' should be listed. <br /> 
<img src="https://i.imgur.com/AKS89Fl.png" height="80%" width="80%" alt="Verifying Windows 10 Client Joined Active Directory Domain"/>
<br />
7. Finally, on the Domain Controller, open DHCP and navigate to 'Address Leases' in the left sidebar. The assigned IP address and DHCP lease details for the Windows 10 client should be displayed, confirming proper functionality. <br /> 
<img src="https://i.imgur.com/2933q2p.png" height="80%" width="80%" alt="Verifying Windows 10 Client DHCP Lease"/>
<br />
</p>
