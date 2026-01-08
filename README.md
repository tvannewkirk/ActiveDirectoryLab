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
<img width="936" height="757" alt="Screenshot 2026-01-06 010337" src="https://github.com/user-attachments/assets/3cc544f8-1cf3-4703-9615-2987f227e15b" />
</p>
Use the Active-Directory-Lab resource group. Name the virtual machine DC-1. Place the virtual machine within East US 2. Use the Windows Server 2022 image. Make the username labuser and make the password Cyberlab123! Check the boxes that you would like to use an existing Windows Server license and confirming that you have an eligible license.
</br>
<p>
<img width="687" height="800" alt="Screenshot 2026-01-06 011313" src="https://github.com/user-attachments/assets/07645284-411c-4bb8-b6da-ab4b1ee6e1ad" />
</p>
Click next:disks and do not change any settings. Click next:networking and make sure the virtual network is the Active-Directory-VNet network. Leave the rest of the settings as default and then click review+create. Click on create to create the DC-1 virtual machine.
</br>
<p>
<img width="736" height="819" alt="Screenshot 2026-01-06 011740" src="https://github.com/user-attachments/assets/6fbfcee3-be30-47d7-a9a1-655a80a11a3d" />
</p>
Search for virtual machines in the search bar and then click on create. Then, click on Azure Virtual Machine.
</br>
<p>
<img width="936" height="757" alt="Screenshot 2026-01-06 010337" src="https://github.com/user-attachments/assets/a9fbc90c-5e71-4cce-824f-bccd659558e4" />
</p>
Assign the virtual machine to the Active-Directory-Lab resource group. Name the virtual machine Client-1. Place the virtual machine in the East US 2 region. Select Windows 10 Pro for the image. Make the username labuser and the password Cyberlab123!. Check the box that you have a Windows 10 license and then click on next:disks.
</br>
<p>
<img width="688" height="824" alt="Screenshot 2026-01-06 012632" src="https://github.com/user-attachments/assets/b9e12d28-a9df-434b-a148-43c5467b4b1f" />
</p>
Click on next:networking. Assign the virtual machine to the Active-Directory-VNet network. Assign the virtual machine the default subnet. Click on review+create. Click on create to deploy the virtual machine.
</br>
<p>
<img width="759" height="853" alt="Screenshot 2026-01-07 135052" src="https://github.com/user-attachments/assets/8a022646-ebd7-4101-be62-15a599525cdb" />
</p>
Search virtual machines in the search bar and click on virtual machines. Click on DC-1. Click on the networking tab on the left and then network settings. Click on the network interface/IP configuration link.
</br>
<p>
<img width="1140" height="382" alt="Screenshot 2026-01-07 135902" src="https://github.com/user-attachments/assets/7dd7652e-b5fd-4f0f-87f2-286f5c9a6ed3" />
</p>
Click on ipconfig1. Select static allocation beneath private IP address settings. Then click save.
</br>
<p>
<img width="588" height="436" alt="Screenshot 2026-01-07 140143" src="https://github.com/user-attachments/assets/faab9183-64d6-4aac-9ad2-38a8083165cd" />
</p>
Navigate back to virtual machines by searching for it in the search bar. Copy the public IP address. Open the Microsoft Remote Desktop application and click on the plus symbol and then click add PC. Paste the IP address into the PC name and make the friendly name DC-1. Click add to add the connection. Click on DC-1. Enter labuser as the username and Cyberlab123! as the password.
</br>
<p>
<img width="397" height="162" alt="Screenshot 2026-01-07 150323" src="https://github.com/user-attachments/assets/09dc6e7a-027a-4207-b071-77b2abf0650a" />
</p>
Inside the domain controller, right click the Windows icon. Click run then type wf.msc to open firewall settings.
</br>
<p>
<img width="377" height="205" alt="Screenshot 2026-01-07 150619" src="https://github.com/user-attachments/assets/b33a3fcf-b9f8-42c9-952b-5d2ee75ebc18" />
</p>
Click on Windows Defender Firewall Properties and type 'o' to turn off the firewall. Click apply then OK.
</br>
<p>
<img width="365" height="417" alt="image" src="https://github.com/user-attachments/assets/f852d5ed-927f-442f-bf50-ae9bd05d7f58" />
</p>
Go to virtual machines within Azure. Click on DC-1. Copy the private IP address under properties and networking.
</br>
<p>
<img width="409" height="347" alt="Screenshot 2026-01-07 151217" src="https://github.com/user-attachments/assets/e6977574-0d47-4db6-ab94-ddbc133b3f52" />
</p>
Click on Client-1 within virtual machines. Click on the Networking tab on the left, then click on Network Settings. Click on the name for the Network Interface.
</br>
<p>
<img width="484" height="93" alt="Screenshot 2026-01-07 151515" src="https://github.com/user-attachments/assets/c79da53c-6b19-4e35-9614-23a7a8bc8642" />
</p>
Click on the DNS Servers tab on the left. Click on Custom under DNS servers. Paste the Private IP Address for DC-1. Click on Save.
</br>
<p>
<img width="684" height="488" alt="Screenshot 2026-01-07 152640" src="https://github.com/user-attachments/assets/33a55994-7a77-45e9-a888-9611b5ad88a9" />
</p>
Navigate back to virtual machines within Azure. Check the box next to Client-1. Click on Restart and then click Yes.
</br>
<p>
<img width="770" height="113" alt="Screenshot 2026-01-07 153013" src="https://github.com/user-attachments/assets/2f7446cb-4e6b-4dc2-95d9-2952ca659739" />
</p>
Navigate back to virtual machines by searching for it in the search bar. Copy the public IP address for Client-1. Open the Microsoft Remote Desktop application and click on the plus symbol and then click add PC. Paste the IP address into the PC name and make the friendly name Client-1. Click add to add the connection. Click on Client-1. Enter labuser as the username and Cyberlab123! as the password.
</br>
<p>
<img width="404" height="157" alt="image" src="https://github.com/user-attachments/assets/27eccf8a-d4e8-4a07-aa5e-28cf48d3df65" />
</p>
Navigate to virtual machines within Azure. Click on DC-1. Copy the Private IP Address under Networking.
</br>
<p>
<img width="404" height="163" alt="Screenshot 2026-01-07 153706" src="https://github.com/user-attachments/assets/755c6a17-560b-4f8f-80b1-eddaa2b47b82" />
</p>
Open the Client-1 Remote Desktop connection. Click on the Windows icon and type Powershell and open it.
</br>
<p>
<img width="716" height="450" alt="Screenshot 2026-01-07 153913" src="https://github.com/user-attachments/assets/5b10dfb0-12d0-4730-a5cd-f36fda10fa7f" />
</p>
Type ping and paste the IP address of DC-1. Observe the results.
</br>
<p>
<img width="907" height="403" alt="Screenshot 2026-01-07 154038" src="https://github.com/user-attachments/assets/27e74c32-72d9-4e3e-a8ae-b19eb3a432da" />
</p>
Type ipconfig /all inside of Powershell. Observe the results. DC-1 is the DNS Server for Client-1.
</br>
<p>
<img width="1260" height="571" alt="Screenshot 2026-01-07 154310" src="https://github.com/user-attachments/assets/4538aab0-a1f5-4aad-a942-f2412e085339" />
</p>
Open the DC-1 Remote Desktop connection. Enter the username as labuser and the password as Cyberlab123!.
</br>
<p>
<img width="404" height="157" alt="Screenshot 2026-01-07 153323" src="https://github.com/user-attachments/assets/4ee6c65a-3eed-4eeb-bfd7-8bfda97fa6c3" />
</p>
Click on the Windows icon and then click on Server Manager. Click on add roles and features.
</br>
<p>
<img width="1119" height="801" alt="Screenshot 2026-01-07 174243" src="https://github.com/user-attachments/assets/04f007d8-aac2-4348-b0e2-1863a0022fec" />
</p>
Click next three times within the wizard. In the Server Roles section click on Active Directory Domain Services. Click on next.
</br>
<p>
<img width="725" height="511" alt="Screenshot 2026-01-07 174531" src="https://github.com/user-attachments/assets/27571d45-e5a6-48a8-a45d-1c1950c8b97e" />
</p>
Click on next two more times. In the Confirmation section, click on Restart the Destination Server if Required. Click on install.
</br>
<p>
<img width="721" height="512" alt="image" src="https://github.com/user-attachments/assets/d339ff58-a4b9-4e00-9361-27f841323161" />
</p>
Within Server Manager, click on the flag icon at the top right. Click Promote this Server to Domain Controller.
</br>
<p>
<img width="373" height="298" alt="Screenshot 2026-01-07 175031" src="https://github.com/user-attachments/assets/839dcd2d-e8fc-4207-bbf7-2c247b01cd80" />
</p>
Select add a new forest. Enter the root domain name as mydomain.com. Click on next.
</br>
<p>
<img width="696" height="507" alt="Screenshot 2026-01-07 175348" src="https://github.com/user-attachments/assets/82443a9b-8874-4dbf-a41c-69343eb6dbf6" />
</p>
Make the Directory Services Restore Mode password Password1. Click on next.
</br>
<p>
<img width="690" height="508" alt="image" src="https://github.com/user-attachments/assets/1d714f29-fbc7-4e41-a061-e27ed79f0b98" />
</p>
Click on Prerequisite Checks on the left side and then click install.
</br>
<p>
<img width="694" height="515" alt="Screenshot 2026-01-07 210848" src="https://github.com/user-attachments/assets/a5047da5-d78a-46e3-a816-0eb45e57eb55" />
</p>
After the virtual machine restarts, click on the DC-1 remote desktop connection and login using the mydomain.com\labuser username and Cyberlab123! password.
</br>
<p>
<img width="396" height="142" alt="Screenshot 2026-01-07 211541" src="https://github.com/user-attachments/assets/b8fc6934-4264-45cf-87a4-526a4dc3dd45" />
</p>
Click on the Windows icon. Then click on Administrative Tools and Active Directory Users and Computers.
</br>
<p>
<img width="593" height="583" alt="Screenshot 2026-01-07 212124" src="https://github.com/user-attachments/assets/d152ce5b-b5d9-4ffb-81a9-cda12b73b049" />
</p>
Click on the arrow next to mydomain.com on the left side. Right-click mydomain.com, mouse over new and click on Organizational Unit. Name the Organizational Unit _EMPLOYEES. Click OK.
</br>
<p>
<img width="783" height="595" alt="image" src="https://github.com/user-attachments/assets/a00aa41c-ac6d-459c-a9d2-390eb0080bd1" />
</p>
Right-click mydomain.com and mouse over new and click on Organizational Unit. Name the Organizational Unit _ADMINS. Click OK.
</br>
<p>
<img width="787" height="531" alt="image" src="https://github.com/user-attachments/assets/faa096a4-01bd-49a6-b8c3-65c5e04472a5" />
</p>
Click on the _ADMINS Organizational Unit. Right-click in the blank area, mouse over new and select user. Name the user Jane Doe. Make the user logon name jane_admin. Click next.
</br>
<p>
<img width="790" height="597" alt="Screenshot 2026-01-07 213121" src="https://github.com/user-attachments/assets/63b3a7f2-0790-4aab-825a-ba289e344a02" />
</p>
Make the password Cyberlab123!. Uncheck user must change password on next logon. For lab purposes, select password never expires. Click on next. Click on finish.
</br>
<p>
<img width="784" height="588" alt="Screenshot 2026-01-07 213347" src="https://github.com/user-attachments/assets/9c87da9d-df03-47ff-a98d-4aa1c426f7a9" />
</p>
Right-click Jane Doe's account and select properties. Select member of. Click add and type domain admins into the blank field and select check names. Click OK.
</br>
<p>
<img width="562" height="309" alt="Screenshot 2026-01-07 213730" src="https://github.com/user-attachments/assets/9eeabe1c-c4d0-45e1-bb79-af7e2ef4c666" />
</p>
Right-click the windows icon and select run. Type logoff and click OK to log out.
</br>
<p>
<img width="377" height="203" alt="Screenshot 2026-01-07 214044" src="https://github.com/user-attachments/assets/46f9962c-5f82-49d9-8d5d-b6262f2db729" />
</p>
Re-open the connection to DC-1. Enter mydomain.com\jane_admin as the username and Cyberlab123! as the password.
</br>
<p>
<img width="406" height="216" alt="Screenshot 2026-01-07 214235" src="https://github.com/user-attachments/assets/649211f3-3888-49c5-b13d-7a072fd273e7" />
</p>
Open the Remote Desktop connection to the Client-1 virtual machine. Enter labuser as the username and Cyberlab123! as the password.
</br>
<p>
<img width="397" height="162" alt="Screenshot 2026-01-07 150323" src="https://github.com/user-attachments/assets/dffb4c6b-f2df-43ee-bb40-2a1daa2287b4" />
</p>
Right-click the Windows icon and select System. Click on Rename this PC (advanced). Click on change within the Computer Name tab. Select domain under member of and enter mydomain.com and click OK.
</br>
<p>
<img width="374" height="428" alt="image" src="https://github.com/user-attachments/assets/1a2e5da1-732a-4162-9bcb-fb7fe5eebcff" />
</p>
Enter mydomain.com\jane_admin as the username and Cyberlab123! as the password. Click OK. Client-1 is now joined to the domain. Restart Client-1.
</br>
<p>
<img width="417" height="269" alt="Screenshot 2026-01-07 215514" src="https://github.com/user-attachments/assets/8a06db05-215f-41ee-b685-2fc4b0bcec9f" />
</p>
<p>
<img width="274" height="137" alt="Screenshot 2026-01-07 215610" src="https://github.com/user-attachments/assets/1d646ae4-2d89-4f94-850f-c477aea9e8e5" />
</p>
In the DC-1 connection, search Active Directory Users and Computers in the search bar and open it. Click the arrow next to mydomain.com and click on Computers and verify that Client-1 is present.
</br>
<p>
<img width="928" height="447" alt="Screenshot 2026-01-07 220004" src="https://github.com/user-attachments/assets/c64b0100-62a5-4ebd-8f25-d31d11927730" />
</p>
Right-click mydomain.com. Mouse over new and select Organizational Unit. Name the Organizational Unit _CLIENTS and click OK.
</br>
<p>
<img width="555" height="478" alt="Screenshot 2026-01-07 220408" src="https://github.com/user-attachments/assets/2e58b63f-49ed-4a81-9492-2c158d25fc1a" />
</p>
Click on the Computers Organizational Unit and drag the Client-1 computer into the _CLIENTS Organizational Unit.
</br>
<p>
<img width="1091" height="550" alt="Screenshot 2026-01-07 220604" src="https://github.com/user-attachments/assets/789e3adf-4b8a-438c-ad1e-7e8a34677bb3" />
</p>
Open the connection to Client-1. Log in using mydomain.com\jane_admin as the username and Cyberlab123! as the password.
</br>
<p>
<img width="396" height="142" alt="Screenshot 2026-01-07 211541" src="https://github.com/user-attachments/assets/08dfe3aa-7af5-4872-98f6-d7b22e35aaa5" />
</p>
Right-click the Windows icon and select System. Click Remote Desktop on the right. Click Select Users that can Remotely Access this Account under User accounts. Click Add. Enter domain users and click check names. Click OK.
</br>
<p>
<img width="414" height="228" alt="Screenshot 2026-01-07 221713" src="https://github.com/user-attachments/assets/203ed520-6733-46d5-982d-bd4e123a1196" />
</p>
Open the DC-1 connection. Click the search bar and type Powershell ISE. Open Powershell ISE by right-clicking and opening as Administrator.
</br>
<p>
<img width="714" height="560" alt="Screenshot 2026-01-07 222441" src="https://github.com/user-attachments/assets/814be4d2-ad3b-4ef8-88d3-4d839257e03c" />
</p>
Open the Powershell script which creates the user accounts. Copy the contents. In Powershell ISE, click the file icon at the top left to create a new script. Use ctrl+s and save the file to the Desktop. Name the file create-users.
</br>
<p>
<img width="818" height="508" alt="Screenshot 2026-01-07 222837" src="https://github.com/user-attachments/assets/18288803-1004-44b3-b564-e1d1a2f03971" />
</p>
Paste the script into the new file. Click the play button to run the script. Click OK.
</br>
<p>
<img width="437" height="113" alt="Screenshot 2026-01-07 223122" src="https://github.com/user-attachments/assets/fb8ef527-f943-4abf-9624-39c85a019e28" />
</p>
In the Client-1 connection, log out of Jane Doe's account. Re-open the connection and log in using mydomain.com\(new user's name) and Password1 as the password. You are now logged into the domain using one of the created accounts.
</br>
<p>
<img width="937" height="652" alt="Screenshot 2025-12-11 231111" src="https://github.com/user-attachments/assets/bc101072-2385-4835-818a-d16a08ead412" />
</p>
<p>
<img width="1098" height="634" alt="Screenshot 2025-12-11 230903" src="https://github.com/user-attachments/assets/eb8373db-717f-4e29-9bd3-2eabaef3ad7a" />
</p>










