<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket. The project demonstrates the osTticket help desk system in a cloud-hosted enviornment by using Microsoft Azure.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)
- osTicket
- MySQL
- Heidi
- PHP

<h2>Operating Systems Used </h2>

- Windows 11 for Desktop
- Windows 10 for Virtual Machine</b> (22H2)

<h2>List of Prerequisites</h2>

- Azure Subscription
- Azure Virtual Machine
    - OS: Windows 10
    - vCPUs: 2
- Remote Desktop Connection
  
<h2>Installation Steps</h2>

### Step 1: Create and Configure the Azure Virtual Machine
<p>
<img width="1837" height="846" alt="image" src="https://github.com/user-attachments/assets/d4526df4-3ff5-48fc-b2f1-aa3bc52d23d3" />

</p>
<p>
Logged into Azure to start creating my enviornment for osTicket. Created a Resource Group called "osTicket" for where the Virtual Machine and Virtual Network will be located.
</p>
<br />

<p>

<img width="1868" height="879" alt="581001344-6e13ea6d-bf7f-48e1-82af-092d9ad8f3d9" src="https://github.com/user-attachments/assets/7fe18a04-30bf-47a4-bf42-47f3724bacc3" />

</p>
<p>
After creating the resource group I needed to create a virtual network for my setup on the Virtual Machine. I called the network "ticket-vnet" and put it into the resource group.
</p>
<br />

<p>
<img width="1874" height="881" alt="image" src="https://github.com/user-attachments/assets/8de4c4a8-9a73-4284-bac0-17cbccdc6670" />
</p>
<p>
Creating a Virtual Machine called "ost-vm". Using the resource group made before (osTicket) and put it there. I'm also using "West US 2" as my region because that is closest to me for quicker feedback, but can be done in a different Region. 
</p>
<br />

<p>
<img width="1142" height="542" alt="image" src="https://github.com/user-attachments/assets/e9d5b76a-9a96-4e71-9143-459e593b1dd8" />
</p>
<p>
For the Image/OS I used Windows 10 Enterprise, version 22H2 - x64 Gen2. For Size I used Standard L2s v4 (2 vcpus, 16 GiB memory).

<p>
<img width="1870" height="879" alt="image" src="https://github.com/user-attachments/assets/0da4fb5a-2c73-48d3-9af2-9259f71dd623" />
</p>
<p>
For logging into the Virtual Machine you need a Username and Password. 
    
    - Username: labuser
    - Password: Cyberlab123!

Since I'm using a Windows 10/11 OS I need to check the licensing at the bottom. The usernames and passwords I use are for this project only. Its never good to store your passwords in plain text.
</p>
<br />

<p>
<img width="1870" height="882" alt="image" src="https://github.com/user-attachments/assets/004193b7-3560-4c90-b98d-9bc900493a07" />
</p>
<p>
Went to the Networking tab and verified that my Virtual Network is selected to "ticket-vnet". Then I went to the Review + Create tab to finish my Virtual Machine. 
</p>

### Step 2: Getting osTicket Files and Dependicies
<p>
<img width="976" height="566" alt="image" src="https://github.com/user-attachments/assets/b86befaf-0299-4309-8bf6-23841941cb09" />
</p>
<p>
Go to the windows search bar to open up "Remote Desktop Connection". Copy + Paste the public IP address of the virtual machine to connect. Enter the username and password used during the setup process. 
</p>
<br />

<p>
<img width="362" height="156" alt="image" src="https://github.com/user-attachments/assets/3beb0b89-e320-4d23-9b42-3e11a04ccbb6" />
<img width="135" height="221" alt="image" src="https://github.com/user-attachments/assets/bae53f78-9405-4375-b3c3-8e0fec4d0a32" />
</p>
<p>
Inside the VM download the required osTicket Installation Files and saved them locally to the desktop. Extracted the contents of the file named "osTicket-Installation-Files". 
</p>
<br />

### Step 3: Install and Enable IIS with CGI. (Web Server)

<p>
<img width="1118" height="628" alt="image" src="https://github.com/user-attachments/assets/83f7eded-fa32-4f2f-bfff-8f4b1aea776b" />
<img width="1121" height="626" alt="image" src="https://github.com/user-attachments/assets/3d157a89-a727-4b91-9638-9e41be789ca3" />
<img width="412" height="369" alt="image" src="https://github.com/user-attachments/assets/d0b1b74c-6126-47ae-be85-c3a02d3a791e" />

</p>
<p>
Go to the start menu and open the control panel. Then click on programs -> Programs and Features -> Turn Windows features on or off.
</p>
<br />

<p>
<img width="1123" height="630" alt="image" src="https://github.com/user-attachments/assets/fc195a79-7c5f-447a-87a3-9bcd81fa0f86" />
<img width="450" height="425" alt="image" src="https://github.com/user-attachments/assets/ec4a08f1-4ca3-4131-ba63-7549ac2e27d7" />
</p>
<p>
Enable Internet Information Services. Go to Internet Information Services -> World Wide Web Services -> Application Development Features -> Enable CGI. This will support PHP processing and prepare the server environment for osTicket deployment.

    - Note: You can go to a browser and enter the loopback IP address 127.0.0.1 to verify that the web server setup worked.

<img width="918" height="947" alt="image" src="https://github.com/user-attachments/assets/5a0a3419-752d-4788-b8dc-556ed5f2069e" />

</p>
<br />

### Step 4: Installing Required Components for osTicket
<p>
<img width="1118" height="631" alt="image" src="https://github.com/user-attachments/assets/e8cd99ea-25a3-465e-9a14-242d9bf6c4ff" />
</p>
<p>
 From the "osTicket-Installation-Files" folder install "PHPManagerForIIS_V1.5.0".
</p>
<br />

<p>
<img width="1122" height="631" alt="image" src="https://github.com/user-attachments/assets/60fc0578-5637-46e3-b147-1d5e04733690" />
</p>
<p>
 From the "osTicket-Installation-Files" folder install "rewrite_amd64_en-US".
</p>
<br />

<p>
<img width="1122" height="634" alt="image" src="https://github.com/user-attachments/assets/063dba2c-6614-4ca6-924b-575019a98f26" />
</p>
<p>
 Open File Exploer and open your C-Drive (This PC -> Windows C:) to create a new folder called PHP. 
</p>
<br />

<p>
<img width="1033" height="737" alt="image" src="https://github.com/user-attachments/assets/7c630b1e-c9a0-49d6-9688-48c31660e832" />
</p>
<p>
From the "osTicket-Installation-Files" unzip "php-7.3.8-nts-Win32-VC15-x86" into the PHP folder (C:\PHP).
</p>
<br />

<p>
<img width="1129" height="638" alt="image" src="https://github.com/user-attachments/assets/ac349ea4-b49d-440a-af1d-95571b3ba9f1" />
</p>
<p>
 From the "osTicket-Installation-Files" folder install "VC_redist.x86". This will satisfy runtime dependencies necessary for PHP to function correctly within the IIS environment.
</p>
<br />

<p>
<img width="1118" height="629" alt="image" src="https://github.com/user-attachments/assets/656874fd-266b-4072-bcb8-502b6df9f735" />
</p>
<p>
 From the "osTicket-Installation-Files" folder install "mysql.5.5.62-win32". This is a database that osTicket will store all of our data in (User accounts, Ticketing Information, etc.)
</p>
<br />
<p>
<img width="488" height="386" alt="image" src="https://github.com/user-attachments/assets/800b2b4b-e625-4e08-9985-12c56e567e62" />
<img width="492" height="381" alt="image" src="https://github.com/user-attachments/assets/d183eb28-bbef-4966-bc29-429abd31ac6b" />

</p>
<p>
In the setup window select typical and proceed to install. Check the Launch the MySQL Instance Configuration Wizard at the bottom.
</p>
<br />

<p>
<img width="494" height="375" alt="image" src="https://github.com/user-attachments/assets/ce513ac7-c289-4ace-848f-5469789b29dc" />
<img width="494" height="376" alt="image" src="https://github.com/user-attachments/assets/73a43f16-d006-4dcc-8e67-36bfce3237c0" />
</p>
<p>
After clicking next once you want to select Standard Configuration. Click next. Leave the next page alone and click next. 
</p>
<br />

<p>
<img width="496" height="377" alt="image" src="https://github.com/user-attachments/assets/ca6161bc-50cc-4837-b1f2-e5f30b19b275" />
<img width="495" height="382" alt="image" src="https://github.com/user-attachments/assets/5f54e4c2-7d95-4fbf-83b8-97342c37a795" />
</p>
<p>
Configure the database admin credentials using:
    
    - New root password: root
    - Confirm: root

Click next then execute.

    - Note: In real world environments, strong credentials should always be used.
    
</p>
<br />

### Step 5: Configuring Web Server
<p>
<img width="1421" height="750" alt="image" src="https://github.com/user-attachments/assets/96db59ea-99ee-4159-a911-7984a762032c" />
</p>
<p>
Go to the windows search bar and search for "IIS" (Internet Information Services) and run it as admin.
</p>
<br />

<p>
<img width="1420" height="751" alt="image" src="https://github.com/user-attachments/assets/a2bc3b20-5058-4e99-a1a7-14db99efe4f1" />
<img width="1423" height="744" alt="image" src="https://github.com/user-attachments/assets/98a8a8e9-0390-4f42-8747-546a92189ce9" />
</p>
<p>
Open PHP Manager. Register new PHP version then browse to the PHP folder in the C drive and open php-cgi (C:\PHP\php-cgi.exe). This will make the web server aware of PHP on the computer and telling it where it is.
</p>
<br />

<p>
<img width="1423" height="749" alt="image" src="https://github.com/user-attachments/assets/5aad967f-e66a-430e-b201-7a2f36509377" />
<img width="206" height="691" alt="image" src="https://github.com/user-attachments/assets/ba47d2a3-c078-4dae-911f-f0b85199f928" />
</p>
<p>
In IIS go back to the home page and restart the IIS service to apply the changes and ensure the web server properly recognized the newly registered PHP runtime.
</p>
<br />
