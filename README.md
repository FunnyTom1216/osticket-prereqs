<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket. 

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
- Remote Desktop Connection
- osTicket
- MySQL
- Heidi
- PHP

  
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

### Step 6: Installing osTicket

<p>
<img width="1121" height="627" alt="image" src="https://github.com/user-attachments/assets/4260737f-c347-4e8a-af90-ada1e2fafa5d" />
<img width="1124" height="820" alt="image" src="https://github.com/user-attachments/assets/9b2e4420-6065-4f2c-a101-139741648f5c" />
</p>
<p>
Extract "osTicket-v1.15.8.zip" from the osTicket-Installation-Files. Open the extracted folder and copied the upload folder to wwwroot (C:\inetpub\wwwroot). Upload was renamed to osTicket to align with the intended site structure.
</p>
<br />

<p>
<img width="1421" height="747" alt="image" src="https://github.com/user-attachments/assets/9c6ec5b9-768d-4994-a269-4cf28db4605d" />
<img width="916" height="924" alt="image" src="https://github.com/user-attachments/assets/9d2f3028-0b58-4e5c-9dda-a010a42cc9c4" />
</p>
<p>
Reload IIS. In IIS navigate to Sites -> Default Web Site -> osTicket and click on Browse:80(http). This will open osTicket site in your browser and verifies that everything is working properly.
</p>
<br />

<p>
<img width="1419" height="744" alt="image" src="https://github.com/user-attachments/assets/f5381da5-89d5-4803-9fc2-f7b675961504" />
<img width="1419" height="749" alt="image" src="https://github.com/user-attachments/assets/577a07a7-a809-41ad-9ab5-d741248419f1" />
<img width="497" height="255" alt="image" src="https://github.com/user-attachments/assets/55aa2009-7c7b-424c-b30a-fe15c94b0a3c" />
</p>
<p>
Back in IIS go to Sites -> Default Web Site -> osTicket and click into PHP Manager. Go to enable or disable an extension at the bottom of the window. Enable the required PHP extensions php_imap.dll, php_intl.dll, and php_opcache.dll through PHP Manager to ensure full application compatibility and functionality. Refresh the page to verify it worked. 
</p>
<br />

<p>
<img width="1125" height="632" alt="image" src="https://github.com/user-attachments/assets/366cdbf4-a289-496d-bdfb-bd825fe137ad" />
</p>
<p>
Rename the sample configuration file from: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php to C:\inetpub\wwwroot\osTicket\include\ost-config.php.
</p>
<br />

<p>
<img width="915" height="595" alt="image" src="https://github.com/user-attachments/assets/87d72678-f655-4d52-91e9-b996c1ad69b1" />
<img width="912" height="589" alt="image" src="https://github.com/user-attachments/assets/a5550abf-68b8-4cf1-993c-f43dbb1da51c" />
<img width="766" height="517" alt="image" src="https://github.com/user-attachments/assets/c99ed92d-2b82-4b20-b56a-2e4e6dfb7aee" />
</p>
<p>
Assign permissions to ost-config.php by going into properties and disabling inherited permissions and manually adding the appropriate access: Everyone -> Full Control to allow the application to have access and change the file.
</p>
<br />

<p>

<img width="816" height="910" alt="581652591-3895c376-543a-4418-8fe1-e5f989d4e3a6" src="https://github.com/user-attachments/assets/ac64e1c1-6f91-4df2-a05c-b496250e1cd9" />

<p>
Continue setting up osTicket in the browser (Continue). Filled out System Settings, Admin User, and Database Settings. For the Admin User username and password:
    
    - Username: adminuser
    - Password: Password1
</p>
<br />

<p>
<img width="1122" height="629" alt="image" src="https://github.com/user-attachments/assets/d656b7f4-08cf-424b-8fb9-1c72f5d6068c" />
<img width="778" height="606" alt="image" src="https://github.com/user-attachments/assets/48fb1211-2947-4495-b3fa-4abc30387ba6" />
</p>
<p>
Just need to create a dedicated database named osTicket to support the application backend. From the "osTicket-Installation-Files" folder and install HeidiSQL_12.3.0.6589_Setup. Heidi allows access to the database and to configure it. Didn't change any settings and check Launch HeidiSQL.
</p>
<br />

<p>
<img width="683" height="479" alt="image" src="https://github.com/user-attachments/assets/2e88f075-1774-4c62-adc2-f14724a0862d" />
</p>
<p>
Click New and enter the User and Password from the setup of the SQL Server then click open to have a connection to the database.
</p>
<br />

<p>
<img width="931" height="590" alt="image" src="https://github.com/user-attachments/assets/44b476c7-2cbb-459a-a831-16abe1c27cd6" />
</p>
<p>
Went to the top left and right click to Create new -> Database and name it "osTicket". The installation of osTicket will make use of this database and put whatever information/data in there.
</p>
<br />

<p>
<img width="816" height="433" alt="image" src="https://github.com/user-attachments/assets/eed3b75b-f94f-486d-9afc-808fe4164b15" />
</p>
<p>
Back in the browser with osTicket in Database Settings enter:

    - MySQL Database: osTicket
    - MySQL Username: root
    - MySQL Password: root

Click Install!
</p>

<br />

<p>
<img width="914" height="722" alt="image" src="https://github.com/user-attachments/assets/f54c081f-7999-4621-ae8d-80fdf7216539" />
<img width="932" height="592" alt="image" src="https://github.com/user-attachments/assets/cde7c9bc-a964-422b-8aa8-860dc46b080a" />
</p>
<p>
osTicket is now installed! In HeidiSQL in the osticket database there are a tables already created and to store all of the stuff.
</p>
<br />

### Step 7: Login
<p>
<img width="898" height="918" alt="image" src="https://github.com/user-attachments/assets/a4e1f409-2b66-4ab9-9b6a-765d4d88c0e4" />
<img width="899" height="564" alt="image" src="https://github.com/user-attachments/assets/595d7dba-a1ef-41cb-8467-0559c14502d8" />
</p>
<p>
http://localhost/osTicket/scp/login.php to login to help desk.
http://localhost/osTicket/ for end users to send tickets.
</p>
<br />

### End of Project
<p>
Hopefully after finishing all these steps there are no errors and everything deployed properly. This demonstrates the configuration of web servers (IIS), PHP, MySQL database integration, security adjustments to make a proper help desk using osTicket. Help desk is now ready to go!
</p>
<br />

