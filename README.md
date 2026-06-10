<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket. 

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computer)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 11 for Desktop
- Windows 10 for Virtual Machine</b> (22H2)

<h2>List of Prerequisites</h2>

- Azure Subscription
- Remote Desktop Connection
- osTicket  [https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD]
- MySQL   [https://drive.google.com/file/d/1_OWh9p7VQLcrB0q_V7qT8yHl0xo5gv7z/view?usp=share_link]
- Heidi   [https://docs.google.com/document/d/1WovrX2DaS9xkfaSr4LXyB4YnnWpXIgPCMMbbfgHmGVw/edit]
- PHP     [http://localhost/osTicket/scp/login.php]

  
<h2>Installation Steps</h2>

### Section 1: Creating a Resource group, a Virtual Network and Virtual Machine 
First create an Azure account or sign in. (https://azure.microsoft.com/en-us)
<p>
<img width="1618" height="587" alt="Screenshot 2026-06-09 191208" src="https://github.com/user-attachments/assets/1f0b0d40-7ad3-4296-bacd-9b84d6971af0" />


</p>
<p>
-Then find and click on the Resource Group tab on the left (Picture 1) then select +Create (Picture 2) 
</p>
Picture 1
</p>
<img width="724" height="462" alt="Screenshot 2026-06-09 192356" src="https://github.com/user-attachments/assets/026b86eb-4c0a-4cf2-a222-04541d58daa9" />

</p>
<p>
Picture 2
</p>
<img width="498" height="343" alt="Screenshot 2026-06-09 195306" src="https://github.com/user-attachments/assets/d8a4965a-c7fc-4a87-b7b8-c7f9ec9ba61a" />


</p>
<p>
-On this screen, your subscription (yellow) may be different but thats okay (select the one available to you). For this project, the Resource Group Name (Green) would be osTicket_Project and the Region (Blue) should automatically select the best fit for you. Once all is filled out, select Review and create button at the bottom of your screen, then create again on the next page. 
<br />

<p>
<img width="732" height="359" alt="Screenshot 2026-06-09 200632" src="https://github.com/user-attachments/assets/aae0e6ab-5924-4af0-a329-78519060fea5" />
</p>
<p>
-Now your Resource Group is made! You may need to refresh the page if it does not show up right away. 
</p>
<br />
<img width="1333" height="288" alt="image" src="https://github.com/user-attachments/assets/fc7db7da-e601-48db-905b-9d26ea3e5759" />
<p>
<p>
-Next we will create a Virtual Machines. From your current screen, in the Azure search bar, search for Virtual Machines. Select the one that just says Virtual Machine. Then select +Create > Virtual Machine to get to the next step. 
</p>
<p>
<img width="648" height="288" alt="Screenshot 2026-06-09 203409" src="https://github.com/user-attachments/assets/2f8d2367-f2be-4e22-90c6-07b67d9f314c" />
</p>
<img width="652" height="390" alt="image" src="https://github.com/user-attachments/assets/ca60c9d7-a5ec-4be9-9167-1cf429b764aa" />
<p>
<p>
-Key things to look for in this sections are: Resource group (Yellow)(make sure the correct group is selected, osTicket_Project), Virtual Machine name (Green) (which will be osTicket-VM), Region (Blue) (best fit for your location, may be different from the one shown on here). 
<p>
<p>
<img width="764" height="399" alt="Screenshot 2026-06-09 204453" src="https://github.com/user-attachments/assets/3fa972e6-c804-4353-a8ec-cbad3e058912" />
<p>
<p>
-More things to keep an eye on are Availability Zone (May be affected by your region, Red), Image (make sure it is either Windows 10 or 11 in the drop down, not Windows server, Blue), Size (Yellow, make sure it has minimum 2 vcpus, 8 GiB memory,)
</p>
<p>
<img width="826" height="511" alt="Screenshot 2026-06-09 205839" src="https://github.com/user-attachments/assets/dcdade8f-f058-4426-92b3-3d4df7758b31" />
<p>
<p>

-For the Administration account, you need a Username and Password (Yellow). We will be using: 
    
    - Username: labuser
    - Password: Cyberlab123!

-Since I'm using a Windows 10/11 OS I need to check the Licensing (Blue) at the bottom. The usernames and passwords I use are for this project only. Its never good to store your passwords in plain text. Then select (Circled) Next: Disk > then select Next again at the bottom of the screen, and this will take you to the Networking tab. 
</p>
<br />
<img width="757" height="642" alt="Screenshot 2026-06-09 210255" src="https://github.com/user-attachments/assets/f6db8c64-7e33-41cf-b4d7-e580842cf630" />
<p>
<p>
<p>

-Once in the Networking tab and verify the Virtual Network is selected to "osTicket-VM-vnet". Finally select Review + Create at the bottom, wait for it to validate. 
</p>
<p>
 <img width="586" height="767" alt="Screenshot 2026-06-09 211123" src="https://github.com/user-attachments/assets/e949fc6e-9cac-4419-890a-11207932c76b" />
<p>
</p>
-Once it is done, click Create at the bottom and you have now finished creating a Resource group and a Virtual Machine.
</p>
____________________________________________________________________________________________________________________________________________


### Step 2: Installing osTicket Files on VM
<p>
In this section we will be using a Remote Desktop Connection (RDC) to connect to our Virtual Machine (VM) that we just created. We will also install osTicket files and Dependencies in the VM.
</p>
<p>
 -Since I am using windows, this step may be different depending on if you are using Mac or Linux. On your taskbar (Windows icon or start menu), you will need to search "Remote Desktop Connection"
</p>
<br />
<img width="380" height="82" alt="Screenshot 2026-06-09 213145" src="https://github.com/user-attachments/assets/0e8613d5-bdcf-4c58-bdd6-ef4a717b2fea" />
<img width="294" height="402" alt="Screenshot 2026-06-09 213319" src="https://github.com/user-attachments/assets/53965a80-76e6-445f-b6d1-c1986ac178de" />
</p>
<p>
<p>
</p>
<p>
-A RDC window will pop up, move it to the side for now while we go back to the VM we created. Without clicking the file, on the far right side, there is a tab labled Public IP Address. We will need this for the RDC window so we can connect to the VM. Copy the Public IP Address and paste them to the drop down in the RDC pop up. 
</p>
<p>
<img width="1360" height="499" alt="Screenshot 2026-06-09 214144" src="https://github.com/user-attachments/assets/ca6b2872-051f-4431-9f36-48b19f99c574" />
</p>
<p>
-On the RDC, click Connect. A security window will pop up asking for credentials. Instead of using your personal account to log in, select More Choices > different account, then you will use the username and password we created earlier. Once entered, click Okay. Another window might pop up if you are on Windows, select yes on the pop up to continue to log in.
    
    - Username: labuser
    - Password: Cyberlab123!
<img width="1051" height="398" alt="Screenshot 2026-06-09 215153" src="https://github.com/user-attachments/assets/a523a04c-e468-4a43-b884-4a0f438cda83" />


</p>
<br />
When you have logged in, you will have successfully conncected your RDC to your VM.  
</p>
</p>
</p>
</p>
-ONce in the VM,  access the internet broswer and download the osTicket-Installation-Files.zip and unzip it onto your desktop. The folder should be called “osTicket-Installation-Files”
<p>

  -We will use the files in this folder to install osTicket and some of the dependencies. (File link is in the List of Prerequisits, same one as below)
</p>
[https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD]
 
</p>
</p>
<img width="967" height="342" alt="0ff13ddd-7d81-45c2-8ede-a0889b6a8846" src="https://github.com/user-attachments/assets/cee2d4d9-267f-48ac-9f84-ac9b07444c86" />
</p>
</p>
</p>
-This window will pop up, click "download anyway", no it is not a virus :)
</p>
</p>
<img width="519" height="171" alt="72c8247c-3f3e-464c-9f09-034624dff7a1" src="https://github.com/user-attachments/assets/0f68aed0-6594-4d2b-a25e-6db84d1e3e8a" />
</p>
</p>
</p>
-Open your downloads, and you should see the zip file you just downloaded. Right click on the file or click Extract all on the right, a new unzipped folder will be created. Step 2 Completed.
</p>
</p>
<img width="886" height="383" alt="fe50d69a-9099-44f5-ab17-c3cc011f39d6" src="https://github.com/user-attachments/assets/c41caa4a-1fe1-4b59-a3d8-db437ba7d792" />
</p>
</p>
__________________________________________________________________________________________________________________
<p>
  
</p>

### Step 3: Install and Enable IIS with CGI. (Web Server)

<p>
<p>
In this Section we will be ilstalling/ enabling IIS in the VM.
<p>
<p>
 
-From the VM, you need to open your control panel from the start menu or the Windows menu.
<p>
<p>
<p>

<img width="727" height="293" alt="Screenshot 2026-06-09 230337" src="https://github.com/user-attachments/assets/1d5f002d-0086-4ab9-af4d-1b41feda6cc2" />
<p>
<p>
<p>

  -Once opened, click on programs -> Turn Windows features on or off 
<p>
<p>
<p>
<img width="448" height="377" alt="581603789-83f7eded-fa32-4f2f-bfff-8f4b1aea776b" src="https://github.com/user-attachments/assets/7f0763cd-9f28-446d-9c66-80167492224a" />
<img width="478" height="300" alt="581604105-3d157a89-a727-4b91-9638-9e41be789ca3" src="https://github.com/user-attachments/assets/12676a5e-6af8-4d98-ba67-8638b98424b2" />
<p>
<p>
<p>
A window will pop up, locate and select the box next to Internet Information Services (IIS), click the expand next to the box and locate the World Wide Web Services -> Application Development Features -> [X] CGI 
</p>
<p>
<img width="418" height="372" alt="581604809-fc195a79-7c5f-447a-87a3-9bcd81fa0f86" src="https://github.com/user-attachments/assets/a0fa9a93-e072-4776-8a8b-68da57cfb0a6" />
</p>
<p>
<img width="450" height="425" alt="581607275-ec4a08f1-4ca3-4131-ba63-7549ac2e27d7" src="https://github.com/user-attachments/assets/f80ffe73-a013-45db-b0df-60ef312f7c01" />
<p>
  
</p>
This will support PHP processing and prepare the server environment for osTicket deployment.

    - Note: You can go to a browser and enter the loopback IP address 127.0.0.1 to verify that the web server setup worked.
<img width="933" height="265" alt="e4f10360-4985-459d-875b-68ce4d9b261a" src="https://github.com/user-attachments/assets/08f9195d-7ef4-4a30-abf8-7146bf45e0a0" />

<p>
<p>
<p>
<p>
<p>
<p>
<p>
<p>
 
</p>
</p>
<br />
_________________________________________________________________________________________________________________
<p>
  
</p>

### Step 4: Installing Required Components for osTicket
<p>
In this part we are going back to the “osTicket-Installation-Files” folder so we can install PHP Manager for IIS, install the Rewrite Module 
</p>
</p>
lets start with PHP, click on flie then proceed to intall
<img width="870" height="452" alt="16ec274c-09b9-40ec-af8d-fa0ea1c58822 pt1" src="https://github.com/user-attachments/assets/f4958ddf-8ce5-408a-be8f-83d535ac918e" />
</p>
</p>
<img width="491" height="404" alt="b27855d6-9aa1-4282-a47f-5fd4ff9f91f7" src="https://github.com/user-attachments/assets/46188178-79b5-45ee-93a4-3b7e634f6b53" />
<img width="497" height="407" alt="2456e397-2b1d-4e73-8eda-f2bde4e45c59" src="https://github.com/user-attachments/assets/97aaad3b-86a4-4d47-af6f-95aff1abb53f" />

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

