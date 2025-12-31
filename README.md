# ActiveDirectoryLab

<h1>Active Directory Virtual Machines Project</h1>

<h2>Project Summary</h2>
I utilized Microsoft Azure to create two virtual machines: one using Windows Server 2019 acting as the domain controller, and another virtual machine using Windows 10 Enterprise acting as a workstation in the domain. First, I opened the settings for the domain controller within VirtualBox and I created two network adapters for the virtual machine. One adapter to connect to the client virtual machine and another adapter to connect to the internet. For the adapter connecting to the internet, I selected NAT for the attachment setting. For the adapter connecting to the virtual machine, I selected internal network for the attachment setting. I clicked start and selected the name of the Windows Server 2019 .iso file which I downloaded from the Microsoft Evaluation Center. This begins the installation process for the server. 
<br/><br/>
I selected Windows Server 2019 Standard Evaluation (Desktop Experience) inside of the Windows Setup wizard. This allows the virtual machine to use a graphical user interface. I chose custom for the installation option and I selected drive 0 for the installation location. Once installation was completed, I selected a password for the Adminstrator account. Then I logged into the virtual machine using the Administrator account. Next, I clicked on the network icon and selected the network and clicked change adapter options. I changed the IP address for the adapter connecting to the internal network to 172.16.0.1 with a /24 mask no default gateway and a DNS server address of 127.0.0.1. 
<br/><br/>
To install Active Directory Domain Services, I navigated to Server Manager and clicked on add roles and features. For installation type, I selected role based installation. For the Server Selection, I selected the name of the server. For server roles, I selected Active Directory Domain Services. Then I confirmed the installation of the Active Directory Domain Services role. Next, I clicked on the flag icon within Server Manager and promoted the server to domain controller. In the Deployment Configuration wizard, I selected add a new forest and named the root domain tannervannewkirk.local. In Domain Controller options, I assigned a Domain Services Restore Mode password and proceeded through the wizard to build the domain. I restarted the machine after being prompted and I logged in using Administrator credentials.
<br/><br/>
I opened Active Directory Users and Computers to create a domain administrator account. Next, I right-clicked the domain name and selected new Organizational Unit and named it ADMINS. I right-clicked the Organizational Unit, selected new User and assigned the user my name. Next, I right-clicked the user, selected Properties, Member Of, Add and typed domain admins to make the account a domain administrator.
<br/><br/>
To install Network Address Translation, I opened Server Manager and selected add roles and features. For Installation Type, I selected role based installation. For Server Selection, I chose the name of the server. For Server Roles, I selected Remote Access. For Role Services, I selected Routing and advanced through the wizard to complete the role installation. I selected Routing and Remote Access inside of Tools within Server Manager. Next, I right-clicked the name of the domain controller and selected Configure and Enable Routing and Remote Access. I selected Network Address Translation. For Network Address Translation settings, I selected use this public interface to connect to the internet and selected the name of the adapter connecting to the Wi-Fi card. I completed the wizard to complete the installation.
<br/><br/>
To install Dynamic Host Configuration Protocol, I opened Server Manager and selected add roles and features. For Installation Type and Server Selection, I followed the same steps as before. For Server Roles, I selected DHCP and selected add features. Then I completed the wizard to install the DHCP role. This allows the domain controller to automatically assign IP addresses to client machines within the domain. Next, I opened DHCP within Tools, right-clicked on the DHCP Server, right-clicked IPV4 and selected new scope. I defined the scope as starting at 172.16.0.100 and ending at 172.16.0.200. I gave the scope a subnet mask of /24. I did not exclude any IP addresses and I specified a lease time of eight days. I selected that I want to configure DHCP options for the scope. For Default Gateway Settings, I entered the IP address of the adapter connected to the client which was 172.16.0.1 and selected add. To finish the configuration, I selected that I want to activate the scope.
<br/><br/>
I created another virtual machine within VirtualBox named Windows 10 Workstation and connected the network adapter to the internal network. For this virtual machine, I used the Windows 10 Enterprise .iso file I downloaded from Microsoft Evaluation Center. Next, I logged into the client virtual machine and right-clicked on the start button. Then I selected System and Rename this PC (advanced). I clicked on change and then selected domain beneath member of and typed the name of the domain. I entered Administrator credentials after being prompted and the client joined the domain successfully.
<br />


<h2>Technologies Used</h2>

- <b>Active Directory</b>
- <b>Microsoft Azure</b>
- <b>Windows Server 2019</b>
- <b>Windows 10 Enterprise</b>




