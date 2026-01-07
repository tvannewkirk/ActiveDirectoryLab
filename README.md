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
<img width="404" height="233" alt="Screenshot 2026-01-07 153706" src="https://github.com/user-attachments/assets/2a42d049-c43b-42cf-8236-543b0a6a8732" />
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








