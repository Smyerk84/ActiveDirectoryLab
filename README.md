<h1>Active Directory Home Lab</h1> 

  

<h2>Description</h2> 

In this project, we are going to walk through how to create an active directory home lab environment using Oracle Virtual Box. Configuring and running this lab will help develop our understanding of how active directory and windows networking works. 

  

<h2>High Level Overview</h2> 

Download and install Oracle Virtual Box. Download and install Windows 10 and Windows Server 2019 ISO. Create our first virtual machine that will be our Domain Controller and house active directory. Give it two network adapters: one to connect to the outside internet and one used to connect to the virtual box private network that the clients will connect to. Install Server 2019 on virtual machine (DC) and assign IP addressing for the internal network. The external will automatically get IP addressing from our home network/router. Name the server, create AD, and name the domain. Configure NAT and Routing so the clients on the private network can reach the internet on the DC. Setup DHCP on DC so that when we create our Win 10 machine it can automatically get an IP address. Run a PowerShell script that will automatically create 1k users in AD. Create another virtual machine and install Win 10. This virtual machine will be connected to the private Virtual Box network.  

  

<h2>Notes</h2> 

For this lab ONLY we will use Password1 for everything password related, do not use in real life. Right Ctrl, delete is our default Ctrl Alt Del to sign into Server 19. Host Key (R ctrl) + home will bring up a menu bar where you can customize screen mode etc. As this lab progresses and about the halfway point, we will assume the user is becoming familiar with Win19 server and server manager with enough repetitions so we will decrease the number of screenshots for visual aid but still give a full typed walk though. VM=Virtual Machine. APIPA=Automatic Private IP Addressing. DNS=Domain Name System. AD=Active Directory. AD DS=Active Directory Domain Services. NIC=Network Interface Card. OU=Organizational Unit. RAS=Remote Access Server. NAT=Network Address Translation 

  

<h2>Languages and Utilities Used</h2> 

  

- <b>PowerShell</b>  

- <b>Oracle Virtual Box</b> 

- <b>Windows Server 19 ISO</b> 

- <b>Windows 10 ISO</b>   

  

<h2>Environments Used</h2> 

  

- <b>Windows 10</b> 

- <b>Windows Server 2019</b> 

  

<h2>Program walk-through:</h2> 

  

<p align="center"> 

Download and install Oracle Virtual Box: <br/>   

<img src="https://i.imgur.com/sVww7Ra.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<br /> 

<br /> 

Download Microsoft Windows Server 2019 ISO file: <br/>  

<img src="https://i.imgur.com/lO32tVp.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<br /> 

<br /> 

Download Microsoft Windows 10 ISO file:  <br/>  

<img src="https://i.imgur.com/1kzAfnw.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<br /> 

<br /> 

Configure Virtual Machine (DC): Note: Bidirectional shared clipboard in advanced settings lets you use ctrl c and ctrl v in between your actual computer and virtual machine. Drag n Drop lets you drag files from your desktop into your virtual machine. <br/>  

<img src="https://i.imgur.com/99mb1Wi.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/gG7TwXK.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/Bwa3Avr.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/dqS7i2Z.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/r3UofDE.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<br /> 

<br /> 

Install Server 2019 ISO file onto DC VM, setup, and sign into server. NOTE: Select the desktop experience for GUI and select custom install. After signing into server and for ease of use go to devices and select insert guest additions CD image. Next, on the desktop go to file explorer/this pc and select Virtual Box guest additions that is listed as a drive. Finally, click on and run VBoxWindowsadditions.amd64 and follow the on screen prompts all the way until choosing to reboot now or later; click on reboot later. <br/>  

<img src="https://i.imgur.com/VvcFqfW.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/8UVrevd.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/dGSEd7z.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>  

<br /> 

<br /> 

Setup IP addressing. Change network adapter settings. NOTE: We will start out by selecting the Ethernet that is connected to the internet and view its status by right clicking on it. In this lab it was Ethernet 2 for me, but just make sure you select the adapter that is the opposite of the one that is unrecognized. <br/>  

<img src="https://i.imgur.com/curRwD6.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/f7girLW.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<br /> 

<br /> 

Rename (R click) the Ethernet adapter that is connected to the internet _INTERNET_ and rename the unrecognized adapter X_INTERNAL_X. NOTE: The unrecognized adapter will have an APIPA address (will start with 169.254.) This APIPA address was automatically assigned to this adapter because a DHCP server was not available. This is how you will know it is the internal adapter. Next R click on X_INTERNAL_X and go to properties. In the menu, double click Internet Protocol Version 4. This will bring you to its general tab where you can assign IP addressing.  <br/>  

<img src="https://i.imgur.com/eD7mrn2.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/NQABNho.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/f48vUDy.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<br /> 

<br /> 

In the general tab use the following address: IP=172.16.0.1 Subnet Mask=255.255.255.0 Default Gateway=Leave blank related to the DC serving as the default gateway. DNS=127.0.0.1 or 172.16.0.1 (Once AD is installed it will automatically install DNS. We can either enter its own IP address 172.16.0.1 or we can enter the loopback address which is 127.0.0.1) Loopback address in IPv4 (127.0.0.1) is a generic address that never reaches the network but instead is looped back through the internal NIC. It allows for a reliable method of testing the functionality of an Ethernet card and its drivers and software without a physical network. <br/>  

<img src="https://i.imgur.com/NFje08v.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<br /> 

<br />  

Rename this VM by R clicking on the window icon at desktop and selecting system. Next, click on rename this PC and give it the name DC (Domain Controller) and restart PC. <br/>  

<img src="https://i.imgur.com/XyKoo8S.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/ozbsC4K.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<br /> 

<br /> 

Install Active Directory Domain Services. Within Server Manager, click on add roles or features. Click next on the add roles or features wizard until you come to the option where you see your DC server and its address; click on this server. In the list of checkboxes, check the box that says Active Directory Domain Services and click on add features. Finally, click next on the installation wizard and then lastly click on install so the AD DS will begin to install. This installation may take a while. When it is finished, close out the wizard. You should now notice a yellow exclamation point next to a flag in the top right-hand corner of your server manager window. Click on this and select 'promote this server to a domain controller.' This is called a post deployment configuration. We have installed AD DS but now we will configure it.   <br/>  

<img src="https://i.imgur.com/mDVjYKn.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/JeZeF1m.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/sjtVuvF.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/vEsFmIp.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/0V430IO.png" height="80%" width="80%" alt="AD Lab Creation Steps"/><br /> 

<br /> 

<br />  

Installing AD DS 'Continued'...Next, within the configuration wizard click on add a new forest and name the root domain name mydomain.com. 'You could name this whatever you'd like.' Click next on the wizard and in the password field we will use Password1 as previously stated. Again, DO NOT use this authentication method in real life. Click next within the wizard until you get to the installation option and install AD DS. Our VM DC will automatically restart after this installation. </br> 

<img src="https://i.imgur.com/oie6aBs.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/sVRkN7M.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/GI3ATmJ.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>  

<br /> 

<br />  

We will now create our own dedicated Admin account. You will notice now that your Windows Server login screen looks different and says MYDOMAIN/Admin. Go ahead and login with our PW. To do this go to start/Windows admin tools/AD users and computers. Within the AD users and computers tab right click on mydomain.com 'this is what we named our domain earlier.' and click on new/organizational unit. Think of this OU as a folder within AD. Name this OU _ADMINS and uncheck the default box underneath. This will create a new folder within mydomain.com. Our newly created folder will now show under the expansion of mydomain.com. R click on this folder and select new/user. Enter your name in the first and last name column. For username we will use a- first letter of your first name and full last name; all lower case. This signifies it is an admin account 'a' and identifies the user by first initial and last name. Click next and use our same PW as planned. Uncheck 'user must change PW at next login and do check 'PW never expires' related to this being a lab environment. Click next and finally click finish. We will now see our newly created account under _ADMINS, BUT we still need to make this an Admin account. To do that R click the profile and go to properties/member of and click on ADD. Next, type in the box provided 'domain admins' and click on check names; there we will see it resolves to Domain Admins. Finally, click on okay and apply. NOW, we have our very own domain admin account. To use, log out and back into DC VM. Instead of using our MYDOMAIN/Admin account click on other user and we will notice at the bottom it now says, 'sign into mydomain.' For this username we will use our newly created a- first letter of your first name and full last name 'all lowercase' and again we will use our PW previously stated. </br> 

  

<img src="https://i.imgur.com/6eQWJ2U.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/lc5gtIN.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/nug9iHA.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/wvQJCWz.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/5qmGqPe.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/qSNV2S5.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 

<img src="https://i.imgur.com/b0ZsEjj.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>  

<img src="https://i.imgur.com/Dpdjdce.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>  

<img src="https://i.imgur.com/3ABHWMH.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>  

<br /> 

<br /> 

Install RAS/NAT. This will allow our future Windows 10 client to be on the private virtual network but still be able to access the internet through the DC. Within server manager click on add roles and features. Click next and confirm server in the box. Checkmark the box that says remote access. Click next and so checkmark the box that says routing. And click next all the way to install and click that. After installation click on tools within server manager and select routing and remote access. Within the routing and remote access box R click on DC (local) and select configure and enable routing and remote access. Within the setup wizard box click next and click the radio button for NAT. click next 'sometimes the box is left blank and not available to select. If this happens cancel this and repeat the previous steps again in hopes that it will behave as intended.' Choose the public facing network interface labeled _INTERNET_ and that used DHCP. Click next and finally click finished. After initializing, the DC (Local) description should visualize as green versus being previously red.  

  

<img src="https://i.imgur.com/e0XHtrv.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>  

<img src="https://i.imgur.com/njfamqV.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>  

<img src="https://i.imgur.com/LyyNf33.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>  

<br /> 

<br /> 

Install DHCP server on DC. This will let our future Win10 clients get an IP address to browse the internet even though they are on a private internal network. Click on add roles and features. Click next x2 and we will notice that in the menu our server's name now has a 'DC' in front of mydomain.com. Click next and check the box for DHCP server. Click next all the way to install and then click that. Once finished close out the window and click on tools at the server manager menu. choose DHCP. (Again, DHCP is to allow clients on our network to automatically receive their IP addresses; our scope will be a range of 172.16.0.100-200 with a subnet mask of 255.255.255.0.) Within the DHCP box expand dc.mydomiain.com and click once on ipv4 to highlight it. Next, right click on it and choose 'new scope,' this will bring up the new scope wizard. Click next. For our scope name we will use our scope range of 172.16.0.100-200. Click next. For our start and stop address again we will input 172.16.0.100 then 172.16.0.200. Length should be set at 24 and subnet mask should be 255.255.255.0. Click next. There will be no exclusions, so click next. This is lease duration; this is how long a computer can have a particular IP address before it needs to be refreshed. (For example, if you were running a Starbucks cafe with high network traffic and multiple users coming and going you would want to have a short lease; 2 hours versus 8 days so your IP addresses would not be tied up with that kind of turnover.) For this AD lab we will just click next. Click yes I want to configure these DHCP options now. Click next. Now, the default gateway we are going to enter here is the NIC of our internal DC; its IP address is 172.16.0.1. This NIC of the DC will act as the default gateway/router for internal clients to reach the internet. After you enter the IP address of the DC's NIC BE SURE to click on ADD. Click next. We will confirm that DNS resolution is listed as mydomain.com, (when we installed AD on DC it automatically installed DNS, so that is the reasoning behind using the DC as our DNS server here.) and BE SURE to confirm that the IP address listed is 172.16.0.1. If it's something different you will need to remove it and add the correct IP. Click next x2, and chose 'yes I want to activate the scope right now.' Click finish. Now, back at the DHCP box R click dc.mydomain.com and chose authorize. Next right click ipv4 and chose refresh. ipv4 and ipv6 should now both be green. If ipv6 is red just click on once to turn green. We now have our DNS, set up.  

  

<img src="https://i.imgur.com/LyyNf33.png" width="80%" alt="AD Lab Creation Steps"/>  

<img src="https://i.imgur.com/Z2UvHOL.png" width="80%" alt="AD Lab Creation Steps"/>  

<img src="https://i.imgur.com/HhLRsW8.png" width="80%" alt="AD Lab Creation Steps"/>  

<br /> 

<br /> 

Add users to AD using our PowerShell script. First, make a configuration that lets us browse the internet from the DC. We would not usually do this in a production environment but in this lab it is fine. Within server manager click on configure this local server. Find IE enhanced security configuration and click on its icon. We will turn this off for Admins and users. The rationale is if this is left on it will spam us with warning messages every time a new page loads.  

  

<img src="https://i.imgur.com/Ru5bNq9.png" width="80%" alt="AD Lab Creation Steps"/>  

<img src="" width="80%" alt="AD Lab Creation Steps"/>  

<img src="" width="80%" alt="AD Lab Creation Steps"/>  

<img src="" width="80%" alt="AD Lab Creation Steps"/>  

  

  

</p> 

  

<!-- 

```diff 

- text in red 

+ text in green 

! text in orange 

# text in gray 

@@ text in purple (and bold)@@ 

``` 

--!> 

 
