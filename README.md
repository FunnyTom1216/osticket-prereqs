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
 - Once finished then proceed to install the Rewrite file
</p>
<br />
<img width="870" height="452" alt="16ec274c-09b9-40ec-af8d-fa0ea1c58822 pt2" src="https://github.com/user-attachments/assets/0345dde8-277a-4e37-b1eb-3b843eadafc9" />
</p>
<p>
<img width="545" height="428" alt="db6e188b-f4c9-4abc-a293-2b0da08e275a" src="https://github.com/user-attachments/assets/25ddd618-25ae-4b81-bf7f-3331664f8037" />
<img width="496" height="385" alt="8016ca41-5c00-4e21-bfa4-606f59053d7f" src="https://github.com/user-attachments/assets/dbfd8d7c-2143-4a8b-9312-ffa77ab3bb1e" />
</p>
<p>
 Open File Exploer and open your C-Drive (This PC -> Windows C:) to create a new folder called PHP. 
<p>
<img width="1122" height="634" alt="image" src="https://github.com/user-attachments/assets/063dba2c-6614-4ca6-924b-575019a98f26" />
</p>
<br />
From the "osTicket-Installation-Files" unzip "php-7.3.8-nts-Win32-VC15-x86" into the PHP folder (C:\PHP) that we had just created.
<p>
</p>
<img width="913" height="334" alt="581618449-7c630b1e-c9a0-49d6-9688-48c31660e832" src="https://github.com/user-attachments/assets/80098843-03bc-4466-b23f-3d52b9b7c8b8" />
</p>
<p>
</p>
 Next from "osTicket-Installation-Files" folder, we are going to install "VC_redist.x86". this dependencie is necessary for PHP to function correctly within the IIS environment.
</p>
</p>
<br />
<img width="656" height="251" alt="d0f39913-a5a2-4ae2-b29f-b3d6eb044123" src="https://github.com/user-attachments/assets/80b50545-d558-444d-bf46-1784fe8bfcef" />
</p>
</p>
Click intall, then close
</p>
</p>
<img width="497" height="314" alt="af18cc2f-d139-44be-817e-71bf44765108" src="https://github.com/user-attachments/assets/95a2cb94-f9a2-4717-a2b9-e9d931c3305a" />
</p>
<br />
<img width="472" height="292" alt="e8dfdfd2-5b99-4555-ba1f-c49e92c87771" src="https://github.com/user-attachments/assets/e9d6a0a8-fb16-4506-855b-cb57bdd31f9a" />
</p>
</p>

From the "osTicket-Installation-Files" folder install "mysql.5.5.62-win32". This is a database that osTicket will store all of our data in (User accounts, Ticketing Information, etc.)
</p>
<p>
<img width="612" height="239" alt="4bb8bac7-45d4-4ec5-89fe-81403f598f6e" src="https://github.com/user-attachments/assets/af3f5ac9-986b-41c2-988b-6b3c3b232c35" />
</p>
<br />
In the setup window select next, then you will select typical and proceed to install. 
<p>
<p>
<img width="493" height="385" alt="278a1a05-1625-4706-81f4-23b80959df2e" src="https://github.com/user-attachments/assets/47947c33-85c5-47fe-beb6-a74f2e6912c6" />
<img width="493" height="380" alt="7b9b997e-aacb-43f0-880f-13270bd11287" src="https://github.com/user-attachments/assets/fe02a940-c5f1-4d48-991c-6f2400e67e63" />
</p>
<p>
Check the Launch the MySQL Instance Configuration Wizard at the bottom.
</p>
<p>
  <img width="493" height="381" alt="d1482c30-01ca-4bb1-8764-8820f09b8aaf" src="https://github.com/user-attachments/assets/c2a2f9ee-bba8-4125-8b5b-d818a36e0366" />
</p>
<p>
A new window will pop up just hit next
</p>
<br />
<img width="495" height="380" alt="7401c3eb-7d18-4ddf-a4c2-c321edc4829f" src="https://github.com/user-attachments/assets/39b7a690-ef5c-41ec-9d39-a8c978ef7286" />
</p>
<p>
Now you are gonna select Standard Configuration. Click next. Leave the next page alone and click next. </p>
<p>
<img width="492" height="381" alt="a2a076ef-aefd-4b77-8cb5-be59ced7c5d8" src="https://github.com/user-attachments/assets/202891d3-6521-424f-b424-3fa9f13a1164" />
<p>
<p>
make sure to check "intall as windows service" box then hit next
</p>
<br />
<img width="494" height="382" alt="b0baaf04-9706-427b-9a00-c63604ae38f6" src="https://github.com/user-attachments/assets/001cfdd8-7e3d-473e-b22a-13a94d59d90f" />
<p>
<p>
Configure the database admin credentials using:
    
    - New root password: root
    - Confirm: root
<p>
<img width="496" height="377" alt="image" src="https://github.com/user-attachments/assets/ca6161bc-50cc-4837-b1f2-e5f30b19b275" />
</p>
<p>

   - Note: In real world environments, strong credentials should always be used.
</p>
<p>
Click next then execute.    
</p>
<br />
<img width="495" height="377" alt="1a752e02-7716-4e27-82e3-307b80a0bf91" src="https://github.com/user-attachments/assets/a6b85c11-8336-46f9-a052-96a406f94e16" />
</p>
<p>
_______________________________________________________________________________________________________________________________________________________________________________
</p>

### Step 5: Configuring Web Server

</p>
<p>
Go to the windows search bar and search for "IIS" (Internet Information Services) and run it as admin.
</p>
<p>
<img width="846" height="371" alt="8bce3e02-3deb-48e4-a28b-064cbfbd5f3b" src="https://github.com/user-attachments/assets/9f32c837-0fca-4e94-a679-696bf8c1b0de" />
</p>
<p>
-Once in it should look like this 
  </p>
<p>
<img width="1421" height="750" alt="image" src="https://github.com/user-attachments/assets/96db59ea-99ee-4159-a911-7984a762032c" />
</p>
<p>
Open PHP Manager.
<p>
  </p>
<img width="561" height="224" alt="581634019-96db59ea-99ee-4159-a911-7984a762032c" src="https://github.com/user-attachments/assets/e592b785-1095-464b-89e2-16412431bae9" />
</p>
<p>
  
<img width="1420" height="751" alt="image" src="https://github.com/user-attachments/assets/a2bc3b20-5058-4e99-a1a7-14db99efe4f1" />
  </p>
<p>
-Register new PHP version
  </p>
<p>
  <img width="807" height="309" alt="581635663-a2bc3b20-5058-4e99-a1a7-14db99efe4f1" src="https://github.com/user-attachments/assets/e4178338-a596-4e0d-b15e-7d63c10ba1a0" />
  </p>
<p>
Then browse to the PHP folder in the C drive and open php-cgi (C:\PHP\php-cgi.exe). This will make the web server aware of PHP on the computer and telling it where it is.
  </p>
<p>
  <img width="1200" height="638" alt="d02bb782-6d08-4292-9af2-bcee0cde4743" src="https://github.com/user-attachments/assets/b7c22b3d-d9ba-49ca-8da8-02aaec3e5ff6" />

<p>
<p>
click ok

<p>
<p>
<img width="1423" height="744" alt="image" src="https://github.com/user-attachments/assets/98a8a8e9-0390-4f42-8747-546a92189ce9" />
</p>
<p>

</p>
<br />
Now in IIS go back to the home page and restart the IIS service to apply the changes and ensure the web server properly recognized the newly registered PHP runtime.
<p>
<p>
<img width="1423" height="455" alt="581637968-5aad967f-e66a-430e-b201-7a2f36509377" src="https://github.com/user-attachments/assets/a8163837-507f-4762-becf-100d2f148bad" />
<p>
<p>
__________________________________________________________________________________________
<p>
  
### Step 6: Installing osTicket

<p>
<p>
-Extract "osTicket-v1.15.8.zip" from the osTicket-Installation-Files. then put the destination of said extraction fold to the folder known as (C:\inetpub\wwwroot). You can copy (C:\inetpub\wwwroot) and paste it into the search when browsing for the file
 <p>
<p>
<img width="835" height="443" alt="4b677bef-9d16-429c-b405-ebe4e983ec92" src="https://github.com/user-attachments/assets/a7f4fd24-9058-4570-869d-3f68fdd212a6" />
</p>
<p>
it should look like this ( note i ended up deleting the scripts fold you only need the upload folder. i forgot to take a new screenshot)
</p>
<br />
<img width="848" height="320" alt="5cc7e567-775a-4f28-9ccd-a39384c701aa" src="https://github.com/user-attachments/assets/f86545d3-ba7c-4d50-a79f-061ac1cca4ce" />
<p>
<p>
- next rename the upload folder to "osTicket"
 <p>
<p>
  <img width="291" height="116" alt="ba7b929b-b77b-4fb9-9297-4043c5f633e8" src="https://github.com/user-attachments/assets/b7a70e7a-c41e-47d4-ae50-94e1e8ff4b05" />
<p>
<p>
 -Reload IIS (Open IIS, Stop and Start the server)
<p>
<p>
  <img width="1423" height="455" alt="581637968-5aad967f-e66a-430e-b201-7a2f36509377" src="https://github.com/user-attachments/assets/31956153-a0d7-40be-9bbb-d01649903126" />
<p>
<p>
  Go to sites -> Default -> osTicket
  <p>
<p>
<img width="413" height="377" alt="581644238-9c6ec5b9-768d-4994-a269-4cf28db4605d pt1" src="https://github.com/user-attachments/assets/d183c989-e193-4622-bfc9-a57a2eb8008a" />
<p>
<p>
On the right, click “Browse *:80”
<p>
<p>
  <img width="1206" height="255" alt="581644238-9c6ec5b9-768d-4994-a269-4cf28db4605d pt2" src="https://github.com/user-attachments/assets/b42f9297-9253-4cb1-8dfb-a47b0100ed8f" />
<p>
<p>
  It should look like this
  <p>
<p>
<img width="916" height="924" alt="image" src="https://github.com/user-attachments/assets/9d2f3028-0b58-4e5c-9dda-a010a42cc9c4" />
</p>
<p>
Now go back into IIS, go to Sites -> Default Web Site -> osTicket and click into PHP Manager. 
</p>
<br />
<img width="576" height="240" alt="581646601-f5381da5-89d5-4803-9fc2-f7b675961504 (1)" src="https://github.com/user-attachments/assets/6f303977-6ea9-4c03-8cc6-b62fcf2dce08" />
<p>
<p>
Go to enable or disable an extension at the bottom of the window.
 <p>
<p>
  <img width="634" height="588" alt="581646601-f5381da5-89d5-4803-9fc2-f7b675961504" src="https://github.com/user-attachments/assets/5e7575d7-0109-454b-97f9-4c03af2a9877" />
<p>
<p>
  From here we are gonna look for the required PHP extensions [php_imap.dll], [php_intl.dll], and [php_opcache.dll] through PHP Manager to ensure full application compatibility and functionality.
  <p>
<p>
<img width="1178" height="587" alt="1cf52229-95e9-4879-8872-68df3469ef14" src="https://github.com/user-attachments/assets/71955fe4-b0b1-458e-bed6-98b7186930b0" />
  <p>
<p>
One all three PHP Extensions are enabled it'll look like this
  <p>
<p>
  <img width="497" height="428" alt="68ecf982-fc2c-496e-8daf-f87c649d94f5" src="https://github.com/user-attachments/assets/fcbd75b0-d8e8-4b8f-aa44-f8ee414eaa3f" />
  <p>
<p>
-Head back to the osTicket installer from eairler to comfirm that it is fully updated
  <p>
<p>
  before
  <p> 
  </p>
  <img width="671" height="355" alt="581645252-9d2f3028-0b58-4e5c-9dda-a010a42cc9c4" src="https://github.com/user-attachments/assets/8eec6095-f2f2-4de2-89c0-336381979fba" />
</p>
<p>
  after
   <p> 
  </p>
  <img width="497" height="255" alt="581647844-55aa2009-7c7b-424c-b30a-fe15c94b0a3c" src="https://github.com/user-attachments/assets/9b993d96-82ee-4a8f-aa45-d24f70089a8f" />
</p>
<br />
Next we are gonna head back into our files, and in the big search bar we are gonna search C:\inetpub\wwwroot\osTicket\include. 
  -the file we will be looking for is [ost-sampleconfig.php]
   <p> 
  </p>
<img width="824" height="622" alt="9e74da22-fc6e-4922-9323-574824ddb109" src="https://github.com/user-attachments/assets/eef6ebca-650a-4f87-a105-1e69cfa7911b" />
 <p> 
  </p>
  once we've found this file we are gonna rename it [ost-config.php] Very important do not include any space when renaming file can just not work afterwards
<p>
</p>
<img width="682" height="157" alt="bb331a79-abea-4568-845e-e3dbb238c3ec" src="https://github.com/user-attachments/assets/fd2b662f-92e8-4041-a795-2e814f02fb15" />
<p>
<p>
We are now going assign permissions to ost-config.php by going into properties and disabling inherited permissions and manually adding the appropriate access: Everyone -> Full Control to allow the application to have access and change the file.
  </p>
<br />
  -On the file we are gonna right click and go to properties
</p>
<br />
<img width="383" height="395" alt="8652cab4-25e5-4099-9ae5-1c132b93d366" src="https://github.com/user-attachments/assets/c0c9f135-6f98-4b57-9244-c7ed34424fb8" />
<img width="401" height="501" alt="0050b7b5-26a7-4d18-8487-3c2e8a38f8a5" src="https://github.com/user-attachments/assets/542de228-9a2c-45ca-8515-d69b24da781f" />
</p>
<p>
  -Then we will check the security tab on the top, and click the "advanced" button to open up special permissions 
</p>
<p>
<img width="382" height="448" alt="5a651615-18c9-40db-adc5-f3a9e1035907" src="https://github.com/user-attachments/assets/b87d766c-9353-43f2-bc2d-bb7ca04682a3" />

</p>
<br />
  -From the security tab: Advance settings, we will click "Disable Inheritance". A security window will pop up asking basically "are you sure, want to remove inherited permissions?" click remove all
<p>
  <p>
<img width="754" height="509" alt="cb54dbb0-a435-44df-9fd3-05ff2512403f" src="https://github.com/user-attachments/assets/eda049e6-e1a5-4b3a-83d6-190303484e96" />
<img width="513" height="269" alt="33b18e9b-2e83-4f55-afb1-ccd88b31ad16" src="https://github.com/user-attachments/assets/e8cbd13e-274e-438b-b982-1ef33d4a5e52" />
<p>
<p>
 -after the Inherited permissions is disable should look like this
<p>
<p>
  <img width="732" height="430" alt="ae0afc64-bede-4e4b-8aa4-875b7d41cb5e (1)" src="https://github.com/user-attachments/assets/52489a55-4455-425b-8635-7d50a086083c" />
<p>
<p>
  -Next we are gonna add new permissions by clicking the "add" 
  <p>
<p>
<img width="205" height="91" alt="020040d9-9bc2-49ab-967f-0153a2a0a9c5" src="https://github.com/user-attachments/assets/1cd04131-3022-43c7-9518-cecf4d07fb48" />
  <p>
<p>
  -From here you will click on "select a principle"
  <p>
<p>
<img width="444" height="429" alt="8d5b2273-7851-4831-a5e6-1998d256a004" src="https://github.com/user-attachments/assets/39e285c3-409d-464a-855d-1b2ef8d108f1" />
  <p>
<p>
  -In the text box you will type Everyone (only for the sake of this project), then click on check names, then hit ok
    <p>
<p>
<img width="458" height="264" alt="429c786e-d178-4fb7-be24-62c10a836759" src="https://github.com/user-attachments/assets/8de821b3-e6a9-4235-b8e6-ce9500392149" />
  <p>
<p>
-Once thats done we are gonna check the "full control" box. then "OK"
  <p>
<p>
<img width="236" height="245" alt="9f807cc4-d582-4435-be74-65303abb69b4" src="https://github.com/user-attachments/assets/45660534-0ecc-41e0-8a52-378171a06167" />
  <p>
<p>
  - We can now press "Apply" then "OK"
  <p>
<p>
<img width="762" height="518" alt="8b2f132c-5886-480b-94b6-8418a000a62a" src="https://github.com/user-attachments/assets/ce3cf555-36b9-402d-9f72-ac7d467c42f4" />
  <p>
<p>

______________________________________________________________________________________________

### Step 7: Completing osTicket settup and Login in

  <p>
<p>
Continue setting up osTicket in the browser "Continue"
   <p>
<p>
<img width="845" height="780" alt="926bdd06-bba5-4298-a2b8-e46d21e55a54" src="https://github.com/user-attachments/assets/afbec0f9-9faf-4c96-95b1-dffd73227d1c" />
 <p>
<p>
  -Filled out System Settings. this can be anything including the name and email (for project sake)
   <p>
<p>
  <img width="642" height="270" alt="9173c9ac-841d-40b0-a5f4-c77b0ae13c27" src="https://github.com/user-attachments/assets/49fd190f-0566-4ed9-85ef-9d43d6ae6275" />
    <p>
<p>
  
  - For Name Again you can put anything as well as for email Just make sureits different from the one you used before. For the Admin User username and password:
    
    - Username: adminuser
    - Password: Password1
</p>
<br />
<img width="504" height="360" alt="22f0cc84-97b1-48e3-9807-f7c41868204b" src="https://github.com/user-attachments/assets/c68c593c-a82b-4238-98ec-f3b3afe87083" />
</p>
<br />
  -When we get to this part we are gonna have to top for a moment. we have to  install HeidiSQL. in order to complete this settup
<img width="613" height="374" alt="25032ba6-adbf-4883-80b9-d01c1b8f13d4" src="https://github.com/user-attachments/assets/579c8222-39d0-4978-80e0-6a6c0d812e07" />
 </p>
<br />
-head back to the “osTicket-Installation-Files” folder, and install HeidiSQL.
<p>
</p>
<img width="796" height="306" alt="b80db95a-1202-44fe-bf4c-dbbf5c67f6ef" src="https://github.com/user-attachments/assets/9f294c11-acac-4128-8f59-cf355a38d379" />
<p>
<p>
  -When you get here one thing you need to make sure is that you accept terms, then to save time mash the next button until you get to the intall. Go ahead and press install
  <p>
<p>
 <img width="583" height="452" alt="844cb56e-a13a-4235-9780-69d840b7f620" src="https://github.com/user-attachments/assets/26c2b391-53a0-4421-8bb7-80b62d122225" />
<img width="582" height="454" alt="5beef299-0182-47d3-9a10-4824053db26f" src="https://github.com/user-attachments/assets/21351e2e-f63f-4997-b61a-e56390b6875f" />
  <p>
<p>
-Once this pops up just make sure the "launch" is check before hiting finish
</p>
<br />
<img width="585" height="457" alt="39cdf920-c5e6-4b75-b3a6-7e729db1c0a8" src="https://github.com/user-attachments/assets/424874ed-a04d-4b52-83ac-f976065a5cbb" />
</p>
<br />
You can press skip to continue
<p>
</p>
<img width="368" height="444" alt="cabcb867-2643-4237-a846-1f08f0457470" src="https://github.com/user-attachments/assets/0369d90f-9a7b-475f-a2d1-85dc99c3b6e1" />
</p>
<br />
Finally when your in HeidiSol, we are gonna click new at the bottom of the screen
</p>
<br />
<img width="470" height="473" alt="2374af77-1aa7-4d56-bdc7-ba7395f3e39b" src="https://github.com/user-attachments/assets/30c5ed31-df48-4586-bc0a-f639390c5a59" />
</p>
<br />
Your page will look like this
</p>
<br />
<img width="915" height="585" alt="5dae9f22-0e40-44e0-930b-aa57cc1a62d2" src="https://github.com/user-attachments/assets/ff0582c3-948a-4e3d-b864-700cf9f0a94f" />
</p>
<br />
Next we are gonna right click UNAMED > CREATE NEW > DATABASE, in that order
</p>
<br />
<img width="475" height="274" alt="1a24b284-51d5-4f4f-9bcc-aea634176a8b" src="https://github.com/user-attachments/assets/ebd44088-59ec-4a71-a7b0-ab5928f298ff" />
</p>
<br /> 
All we gotta worry about is the uuser and password. If you recall from earlier we made the user and password both: root
so that is what we are gonna do here. then press "open"
</p>
</p>
<img width="672" height="444" alt="fa55600f-e8bf-46b6-b168-7b65d76c047e" src="https://github.com/user-attachments/assets/86d2bfe1-8e77-445e-9691-563d588df027" />
</p>
</p>
This will open our connection to our data base
  </p>
</p>
<img width="928" height="583" alt="Screenshot 2026-06-10 152739" src="https://github.com/user-attachments/assets/a13c13d2-0f3a-4d62-9e11-66b94c80546b" />
  </p>
</p>
Now have to create a database called "osticket". so as we did before, right click UNAMED > CREATE NEW > DATABASE, in that order
 </p>
</p>

<img width="475" height="274" alt="1a24b284-51d5-4f4f-9bcc-aea634176a8b" src="https://github.com/user-attachments/assets/ebd44088-59ec-4a71-a7b0-ab5928f298ff" />

 </p>
</p>
Now when this pops up, in the name box is where we will put "osTicket" then press ok
 </p>
</p>

<img width="316" height="251" alt="Screenshot 2026-06-10 152857" src="https://github.com/user-attachments/assets/d9984863-4aea-4b9b-9b95-11606d4dffe1" />
 </p>
</p>
You know its successfull when osTicket tab is now created
 </p>
</p>
<img width="378" height="501" alt="313940bd-b168-428d-8089-ce363ad4b670" src="https://github.com/user-attachments/assets/4c5f1641-ec58-4be8-9a9f-1efa2d9a4da1" />
 </p>
</p>
We can now head back to OSTIcket to finish the settup. Back in the browser with osTicket in Database Settings enter:

    - MySQL Database: osTicket
    - MySQL Username: root
    - MySQL Password: root
Click Install!
 </p>
</p>
<img width="828" height="376" alt="8c0b4931-daa6-4397-9b03-057964a519e9" src="https://github.com/user-attachments/assets/8343684f-ddf6-4082-bbad-96b6eeb246e4" />
 </p>
</p>
Once done it'll say completed (if done properly)
 </p>
</p>
<img width="847" height="668" alt="d4349eb9-9f81-47a8-9d22-2def27f7f2e2" src="https://github.com/user-attachments/assets/e9f52a66-aa09-4ef0-9dba-56108992035c" />
 </p>
</p>
Congratulations, hopefully it is installed with no errors!
-Browse to your help desk login page: (http://localhost/osTicket/scp/login.php)
 </p>
</p>
<img width="1100" height="707" alt="365ecfc1-0b7e-43ec-b612-fb8c8c08dc83" src="https://github.com/user-attachments/assets/4c794e86-ecb4-44ef-8eaf-77bd20c1d845" />
 </p>
</p>
  -End Users osTicket URL: (http://localhost/osTicket/)
   </p>
</p>
<img width="1117" height="617" alt="eeec34ec-ce1c-46dc-a9bd-9646bc9614c3" src="https://github.com/user-attachments/assets/e373c8b2-6f9f-41d2-8008-94918d3805b9" />
 </p>
</p>

### End of Project
<p>
Hopefully after finishing all these steps there are no errors and everything deployed properly. This demonstrates the configuration of web servers (IIS), PHP, MySQL database integration, security adjustments to make a proper help desk using osTicket. Help desk is now ready to go!
</p>
<br />

