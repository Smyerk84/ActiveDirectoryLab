<h1>Active Directory Home Lab</h1>

<h2>Description</h2>
In this project, we're going to walk through how to create an active directory home lab enviroment using Oracle Virtual Box. Configuring and running this lab will definitely help develop our understanding of how active directory and windows networking works.

<h2>High Level Overview</h2>
Download and install Oracle Virtual Box. Download and install Windows 10 and Windows Server 2019 ISO. Create our first virtual machine that will be our Domain Controller and house active directory. Give it two network adapters: one to connect to the outside internet and one used to connect to the virtual box private network that the clients will connect to. Install Server 2019 on virtual machine(DC) and assign IP addressing for the internal network. The external will automatically get IP addressing from our home network/router. Name the server, create AD, and name the domain. Configure NAT and Routing so the clients on the private network can reach the internet on the DC. Setup DHCP on DC so that when we create our Win 10 machine it can automatically get an IP address. Run a powershell script that will automatically create 1k users in AD. Create another virtual machine and install Win 10. This virtual machine will be connected to the private Virtual Box network. 

<h2>Notes</h2>
For this lab ONLY we will use Password1 for everything password related, do not use in real life. Right Ctrl, delete is our default Ctrl Alt Del to sign into Server 19. 

<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Oracle Virtual Box</b>
- <b>Windows Server 19 ISO</b>
- <b>Windows 10 ISO</b>  

<h2>Environments Used</h2>

- <b>Windows 10</b>
- <b>WIndows Server 2019</b>

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
Configure Virtual Machine(DC): Note: Bidirectional shared clipboard in advanced settings lets you use ctrl c and ctrl v in between your actual computer and virtual machine. Drag n Drop lets you drag files from your desktop into your virtual machine. Host Key (R ctrl) + home will bring up a menu bar where you can customize screen mode etc. <br/>
<img src="https://i.imgur.com/99mb1Wi.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>
<img src="https://i.imgur.com/gG7TwXK.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>
<img src="https://i.imgur.com/Bwa3Avr.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>
<img src="https://i.imgur.com/dqS7i2Z.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>
<img src="https://i.imgur.com/r3UofDE.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>
<br />
<br />
Install Server 2019 ISO file onto DC VM, setup and sign into server. NOTE: Select the desktop experience for GUI and select custom install. After signing into server and for ease of use go to devices and select insert guest additions CD image. Next, on the desktop go to file explorer/this pc and select Virtual Box guest additions that's listed as a drive. Finally, click on and run VBoxWindowsadditions.amd64 and follow the on screen prompts all the way until choosing to reboot now or later; click on reboot later. <br/>
<img src="https://i.imgur.com/VvcFqfW.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>
<img src="https://i.imgur.com/8UVrevd.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>
<img src="https://i.imgur.com/dGSEd7z.png" height="80%" width="80%" alt="AD Lab Creation Steps"/> 
<br />
<br />
Setup IP addressing. Change network adapter settings. NOTE: We will start out by selecting the Ethernet that is connected to the internet and view its status by right clicking on it. In this lab it was Ethernet 2 for me, but just make sure you select the adapter that is the opposite of the one that is unrecognized  <br/>
<img src="https://i.imgur.com/curRwD6.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>
<img src="https://i.imgur.com/f7girLW.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>
<br />
<br />
Rename (R click) the Ethernet adapter that is connected to the internet _INTERNET_ and rename the unrecogninzed adapter X_INTERNAL_X. NOTE: The unrecognized adapter will have an APIPA address (will start with 169.254.) This APIPA address was automatically assigned to this adapter because a DHCP server was not available. This is how you will know it's the internal adapter. <br/>
<img src="https://i.imgur.com/NQABNho.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>
<img src="https://i.imgur.com/eD7mrn2.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>
<br />
<br />
Rename this VM by R clicking on the window icon at desktop and selecting system. Next, click on rename this PC and give it the name DC (Domain Controller) and restart PC. <br/>
<img src="https://i.imgur.com/XyKoo8S.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>
<img src="https://i.imgur.com/ozbsC4K.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
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
