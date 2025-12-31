# ActiveDirectoryLab

<h1>Active Directory Virtual Machines Project</h1>

<h2>Project Summary</h2>
I utilized Microsoft Azure to create two virtual machines: one using Windows Server 2019 acting as the domain controller, and another virtual machine using Windows 10 Enterprise acting as a workstation in the domain. First, I created the domain controller virtual machine and named it DC-1. I assigned it a username of labuser and a password of Cyberlab123!. Once the virtual machine was created, I set the private IP address on the NIC to be static and I disabled the Windows Firewall in order to test ping reachability between the domain controller and the client. Then, I created the client virtual machine in Azure which used Windows 10 Enterprise as the operating system. I assigned it a username of labuser and a password of Cyberlab123! and placed it within the same virtual network as DC-1. I assigned Client 1 to use DC-1 as the DNS server. After restarting Client 1, I was able to ping DC-1.
<br/><br/>
<p>
<img width="1175" height="478" alt="Screenshot 2025-12-31 013112" src="https://github.com/user-attachments/assets/46ea6cbb-01eb-4a22-82f9-1a72f7c2a4f8" />
</p>
To install Active Directory Domain Services, I navigated to Server Manager and clicked on add roles and features. For installation type, I selected role based installation. For the Server Selection, I selected the name of the server. For server roles, I selected Active Directory Domain Services. Then I confirmed the installation of the Active Directory Domain Services role. Next, I clicked on the flag icon within Server Manager and promoted the server to domain controller. In the Deployment Configuration wizard, I selected add a new forest and named the root domain mydomain.com.  I restarted the machine after being prompted and I logged in using Administrator credentials.
<p>
<img width="985" height="694" alt="Screenshot 2025-12-11 214114" src="https://github.com/user-attachments/assets/f217649b-6b95-4755-96e7-5bef1aa0f73e" />
</p>
<br/><br/>
I opened Active Directory Users and Computers to create an Organizational Unit called _EMPLOYEES. Next, I created another Organizational Unit and named it _ADMINS. I right-clicked the Organizational Unit, selected new User and called the user Jane Doe. I assigned the account a username of jane_admin and a password of Cyberlab123!. Next, I right-clicked the user, selected Properties, Member Of, Add and typed domain admins to make the account a domain administrator.
<p>
<img width="1170" height="597" alt="Screenshot 2025-12-31 015025" src="https://github.com/user-attachments/assets/7599d45e-671b-47e3-8326-c60469b365a3" />
</p>
<br/><br/>
To install Network Address Translation, I opened Server Manager and selected add roles and features. For Installation Type, I selected role based installation. For Server Selection, I chose the name of the server. For Server Roles, I selected Remote Access. For Role Services, I selected Routing and advanced through the wizard to complete the role installation. I selected Routing and Remote Access inside of Tools within Server Manager. Next, I right-clicked the name of the domain controller and selected Configure and Enable Routing and Remote Access. I selected Network Address Translation. For Network Address Translation settings, I selected use this public interface to connect to the internet and selected the name of the adapter connecting to the Wi-Fi card. I completed the wizard to complete the installation.
<br/><br/>
To install Dynamic Host Configuration Protocol, I opened Server Manager and selected add roles and features. For Installation Type and Server Selection, I followed the same steps as before. For Server Roles, I selected DHCP and selected add features. Then I completed the wizard to install the DHCP role. This allows the domain controller to automatically assign IP addresses to client machines within the domain. Next, I opened DHCP within Tools, right-clicked on the DHCP Server, right-clicked IPV4 and selected new scope. I defined the scope as starting at 172.16.0.100 and ending at 172.16.0.200. I gave the scope a subnet mask of /24. I did not exclude any IP addresses and I specified a lease time of eight days. I selected that I want to configure DHCP options for the scope. For Default Gateway Settings, I entered the IP address of the adapter connected to the client which was 172.16.0.1 and selected add. To finish the configuration, I selected that I want to activate the scope.
<br/><br/>
I created another virtual machine within VirtualBox named Windows 10 Workstation and connected the network adapter to the internal network. For this virtual machine, I used the Windows 10 Enterprise .iso file I downloaded from Microsoft Evaluation Center. Next, I logged into the client virtual machine and right-clicked on the start button. Then I selected System and Rename this PC (advanced). I clicked on change and then selected domain beneath member of and typed the name of the domain. I entered Administrator credentials after being prompted and the client joined the domain successfully.
<br />

<h2>Languages Used</h2>

- <b>Powershell</b>

<h2>Technologies Used</h2>

- <b>Active Directory</b>
- <b>Microsoft Azure</b>
- <b>Windows Server 2019</b>
- <b>Windows 10 Enterprise</b>




