<h1>Active Directory Home Lab</h1>

<h2>Description</h2>
In this project, we're going to walk through how to create an active directory home lab enviroment using Oracle Virtual Box. Configuring and running this lab will definitely help develop our understanding of how active directory and windows networking works.

<h2>High Level Overview</h2>
Download and install Oracle Virtual Box. Download and install Windows 10 and Windows Server 2019 ISO. Create our first virtual machine that will be our Domain Controller and house active directory. Give it two network adapters: one to connect to the outside internet and one used to connect to the virtual box private network that the clients will connect to. Install Server 2019 on virtual machine(DC) and assign IP addressing for the internal network. The external will automatically get IP addressing from our home network/router. Name the server, create AD, and name the domain. Configure NAT and Routing so the clients on the private network can reach the internet on the DC. Setup DHCP on DC so that when we create our Win 10 machine it can automatically get an IP address. Run a powershell script that will automatically create 1k users in AD. Create another virtual machine and install Win 10. This virtual machine will be connected to the private Virtual Box network.



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
Download and install Microsoft Windows Server 2019 ISO file: <br/>
<img src="https://i.imgur.com/lO32tVp.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>
<br />
<br />
Download and install Microsoft Windows 10 ISO file:  <br/>
<img src="https://i.imgur.com/1kzAfnw.png" height="80%" width="80%" alt="AD Lab Creation Steps"/>
<br />
<br />
Install updates for Windows Server 2019: <br/>
<img src=/>
<br />
<br />
Setup IP Addressing: <br/>
<img src="https://i.imgur.com/nCIbXbg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Change the name of this PC:  <br/>
<img src="https://i.imgur.com/cdFHBiU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
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
