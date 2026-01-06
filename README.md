# Active Directory Deployed Within the Cloud
This tutorial demonstrates the creation of an Active Directory domain using Azure virtual machines. 

<h2>Environments Used</h2>

- <b>Active Directory</b>
- <b>Microsoft Azure(Virtual Machines/Compute)</b>
- <b>Remote Desktop</b>
- <b>Powershell</b>


<h2>Operating Systems Used</h2>

- <b>Windows Server 2022</b>
- <b>Windows 10 Enterprise</b>

<h2>Deployment and Configuration Steps</h2>

- <b>Step 1- Create the client and domain controller virtual machines within Azure. Assign the client virtual machine the IP address of the domain controller as the DNS server.</b>
- <b>Step 2- Install Active Directory Domain Services on the domain controller virtual machine and promote it to domain controller.</b>
- <b>Step 3- Join the client virtual machine to the domain.</b>
- <b>Step 4- Allow remote desktop access to the client virtual machine.</b>
- <b>Step 5- Create 10,000 user accounts using a Powershell script and attempt to login with one of the accounts.</b>

<h2>Deployment and Configuration Walkthrough</h2>
Create a new resource group within Microsoft Azure. This resource group is named Active-Directory-Lab and it is located in the East US 2 region.
</br>
<p>
<img width="921" height="840" alt="Screenshot 2026-01-06 004652" src="https://github.com/user-attachments/assets/f82bf72a-1728-48f2-817a-031bfc88270f" />
</p>
Create a virtual network using the Active-Directory-Lab resource group. This virtual network is named Active-Directory-VNet. Click on Review+create and then click on create.
</br>
<p>
<img width="925" height="848" alt="Screenshot 2026-01-06 005513" src="https://github.com/user-attachments/assets/47647b3c-5f10-4518-a27f-16b02e75a400" />
</p>
Search for virtual machines in the search bar and then click on create. Then, click on Azure Virtual Machine.
</br>
<p>
<img width="936" height="803" alt="Screenshot 2026-01-06 010337" src="https://github.com/user-attachments/assets/94e84ada-ef66-47df-a3ac-d92d1bea6503" />
</p>
Use the Active-Directory-Lab resource group. Name the virtual machine DC-1. Place the virtual machine within East US 2. Use the Windows Server 2022 image. Make the username labuser and make the password Cyberlab123! Check the boxes that you would like to use an existing Windows Server license and confirming that you have an eligible license.
</br>
<p>
<img width="687" height="800" alt="Screenshot 2026-01-06 011313" src="https://github.com/user-attachments/assets/07645284-411c-4bb8-b6da-ab4b1ee6e1ad" />
</p>

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
Next, I logged into the Client 1 virtual machine and joined it to the mydomain.com domain by opening settings, clicking on about, then clicking on rename this PC. After this, I clicked change in the computer name tab and I entered mydomain.com in the domain field. Then, I logged in using the Jane Doe admin account within the mydomain.com context and the client joined to the domain.
<p>
<img width="693" height="486" alt="Screenshot 2025-12-31 162941" src="https://github.com/user-attachments/assets/980b8011-25ae-4e46-a010-efe835370375" />
</p>
<br/><br/>
Next, I wanted to allow remote desktop access to Client 1 for non-admin user accounts for troubleshooting purposes. I decided to configure this without the use of group policy. In order to accomplish this, I logged into Client 1 as Jane Doe and opened System Properties and clicked on Remote Desktop. Then, I allowed domain users access by clicking "Select Users that can Remotely Access this PC" and then clicking add. I typed domain users into the field and clicked check names and then clicked OK.
<p>
<img width="342" height="299" alt="Screenshot 2025-12-31 165414" src="https://github.com/user-attachments/assets/f16b5d2e-55b5-4786-902f-482a59b5d1a7" />
</p>
<br/><br/>
I needed to create user accounts for my domain so I logged into DC-1 as Jane Doe, opened Powershell ISE and then I pasted a Powershell script in order to create user accounts with random names. After the script ran, the _EMPLOYEES organization unit contained 10,000 user accounts. I tested the user accounts by logging into Client 1 with one of the accounts I created.
<p>
<img width="937" height="652" alt="Screenshot 2025-12-11 231111" src="https://github.com/user-attachments/assets/96e885b2-4024-46df-a9ec-3f0790e3701b" />
</p>
<p>
<img width="1098" height="634" alt="Screenshot 2025-12-11 230903" src="https://github.com/user-attachments/assets/c246e7bf-619b-4b98-82d9-72e7354c56d4" />
</p>
<br/>



