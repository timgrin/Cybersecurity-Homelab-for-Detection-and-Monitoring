<h1>Cybersecurity-Homelab-for-Detection-and-Monitoring</h1>


<h2>Description</h2>
I approached this Cybersecurity project intending to enhance security by implementing proactive surveillance measures.  This home lab gives a comprehensive walkthrough on configuring, optimizing, and securing IT infrastructure. Although this would be relatively small, the knowledge gained from this can also be applied to real-world enterprises & infrastructures.

<h2>Content</h2>

- Configuring pfsense firewall for Network Segmentation and Security.
- Configuring Security Onion as an all-in-one IDS, security monitoring, and Log Management Solution.
- Configuring Kali Linux as an attack machine.
- Configuring Windows Server as a Domain Controller.
- Configuring Windows Desktop.
- Configuring Splunk.

<h3>Pfsense</h3>
Pfsense will configured as a firewall to segment our private home-lab network and will only be accessible from our Kali Linux machine.

- Click “Create a New Virtual Machine” on the VMware Workstation Home screen.
- Make sure “Typical (recommended)” is selected and click Next.
- Click “Browse” and navigate to the folder where your pfsense file is located.
- Click Next.

<img src="https://imgur.com/cjAJSja.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Rename your Virtual Machine.
- Click “Next”.
- 20GB disk size is sufficient for this VM.
- Ensure that the “Split virtual disk into multiple files” option is selected.
- Click “Next”.
- Click “Customize Hardware”.
- Add 5 network adapters and correspond them with a VMnet interface as shown below. Then click “Finish”.

<img src="https://imgur.com/xSFk8R3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- The pfsense machine will power on and start with this screen. Accept all the defaults. pfsense will configure and reboot.
- You should end up with a screen like this. As shown below.

<img src="https://imgur.com/mxlf5an.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br />
<b>Interface assignment</b> <br />

- Enter option 1 to assign interfaces.
- Should VLANS be set up now [y:n]?: n
- Enter em0, em1, em2, em3, em4 & em5 respectively for each consecutive question
- Do you want to proceed [y:n]?: y

<img src="https://imgur.com/1RPDGRn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Enter option 2
- We’ll start with the LAN interface (2)
- The IP address 192.168.1.1 is going to be used to access the pfsense WebGUI via the Kali Machine
- Assign IP addresses to the interfaces
- Leave the OPT3 interface without an IP as it is going to have the span port with traffic that Security Onion will be monitoring

<img src="https://imgur.com/2MomZzC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<h3>Security Onion</h3>
This will be the all-in-one IDS, Security Monitoring, and Log Management solution.

- Select Typical installation >> Click “Next”
- Installer disc image file >> SO ISO file path >> Click “Next”
- Choose “Linux”, “CentOS 7 64-Bit” and click “Next”.
- Specify the virtual machine name and click Next.
- Click “Customize Hardware” 
- Change memory to 4-32GB
- Add two Network Adapters and assign them Vmnet 4 & Vmnet 5 respectively

<img src="https://imgur.com/jDz2G4G.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click “Finish”
- Power the virtual machine and click Enter when prompted
- After the initial stages of loading, type “yes” when prompted
- Set a username & password
- After Security Onion Reboots, Enter the username & password
- Select “Yes”
- Select “Install”
- Select the EVAL option
- Type “AGREE”
- Select “Standard”
- Set a hostname and a short description
- Click the spacebar to select ens33 as the management interface
- Set the addressing to DHCP
- Select “YES” at the next prompt
- Select “OK” at the next prompt
- Select “Direct” for the next prompt
- Select “ens35” as the Monitor Interface
- Select “Automatic” for the OS patch schedule”
- Accept the default home network IP
- Accept all the defaults
- Enter an email address and password for the admin account
- Select “IP”
- Select “Yes” for the NTP server & accept the defaults

<b>Take note of your final settings before proceeding! The most important detail is the IP address for web access. This will be used to access Security Onion.</b>

<img src="https://imgur.com/X2hskAy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Select “Yes”

After installing Security Onion, having access to the web interface will be done from an external Ubuntu Desktop simulating a SOC/Security Analyst accessing a SIEM or any other tool from their device.

- Use sudo so-allow to create a rule on security onion to allow the ubuntu-desktop
- Grab the IP address on the Ubuntu desktop

<img src="https://imgur.com/vCD8bW2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Run sudo so-allow 

<img src="https://imgur.com/KMF9AJc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Choose the option “a” (analyst)
- Input the “Ubuntu desktop IP address”
  
Then log in to Ubuntu using the security onion web login address

<img src="https://imgur.com/QpeLeXW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/PnoZplv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


<h3>Kali Linux</h3>
Kali Linux will be used as an attack machine to propagate different offensive actions against the Domain Controller and the other attached machines.


- Configure the Kali machine 
- Add network adapter as VMnet2

<img src="https://imgur.com/uFPtBot.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Change the default password

<img src="https://imgur.com/rEl3zct.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Log into pfsense GUI using the web browser on Kali and IP address 192.168.1.1 (pfsense web access address)
- Use the default username “admin” and password “pfsense”

<img src="https://imgur.com/5EhyrUh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Add 8.8.8.8 as your Primary DNS Server
- Add 4.4.4.4 as your Secondary DNS Server
- Untick the last two options

<img src="https://imgur.com/yBkvwgo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br>
<b>Assign interfaces on pfsense</b> <br />

- Click on interfaces
- Select LAN
- Use the below settings and save
-	Repeat the process for other interfaces

<img src="https://imgur.com/E9lgejr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/GkNKOpR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/XvlnB1X.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/ZAGjh02.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/YNzTrSF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/qPAlCSB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Back at Interfaces Assignment select “Bridges”
- Click “Add”
- Select the victim network as the member interface
- Then select “Display Advanced”
- Under Advanced Configuration for Span Port, select “SPANPORT”
- Scroll down and Click “Save”

<img src="https://imgur.com/2h1zFhV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/uksnCZB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click Firewall >> Rules
- Under “edit Firewall Rule” for Protocol select ANY and Save


<img src="https://imgur.com/ViwIdzR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/TbpquxV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<h3>Windows Server Controller </h3>
The goal of this portion of the lab is to set up an Active Directory domain with a Windows 2019 Server as the Domain Controller and a Windows 10 machine.

- Configure the network adapter to VMnet3

<img src="https://imgur.com/vC5xKLr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Install Windows Server 2019

<img src="https://imgur.com/o8E1QZN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Choose to install the Standard Evaluation(Desktop experience)

<img src="https://imgur.com/iJBtM0C.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Rename Domain Controller and reboot
- Open up Server Manager >> Click manage >> Add roles and features

<img src="https://imgur.com/OF1XHbh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Under "Select installation type"
- Keep clicking "Next" till you get to the Server Roles menu
- Select "Active Directory Domain Services"
- Select “Add Features”

<img src="https://imgur.com/Zdd2y1v.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/AD2xJ8A.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/nZwDYTJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click on "Next" till you get to the Confirmation menu, then click "Install"
- After the Install, Click "Close"
- Click on the flag with the yellow caution triangle

<img src="https://imgur.com/acVWrEn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Select "Promote this server to a domain controller"
- Select "Add a new forest"
- Specify a domain name
- Click "Next"
- Set a Password

<img src="https://imgur.com/WYwTy5T.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/gqIQ750.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Select "Active Directory Certificate Services"
- Select "Add Features"
- Click "Next" till you get to the Confirmation menu
- Check "Restart the destination server automatically if required"
- Select "Yes"
- Select "Install"
- After the Installation, Click "Close"
- Click on the flag with the yellow caution triangle
- Select "Configure Active Directory Certificate Services on the destination server"

<img src="https://imgur.com/s2E1dem.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click "Next" on Credentials
- On the Role Services menu, check "Certification Authority"

<img src="https://imgur.com/o38aVvo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click "Next" till you get to the Confirmation menu
- Then select "Configure"

<img src="https://imgur.com/wVjFJ6R.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Manually restart the server for all the settings to take effect
- Add new Users:
- Back at the Server Manager Select Tools >> Active Directory Users and Computers

<img src="https://imgur.com/zvdVAj6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Click on the Domain controller name (homelab.local) >> Click New >> Click User
- Enter a First, Last, and User logon name for the user

 <img src="https://imgur.com/gEz64Yb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/BeUjqJC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Turn off the firewall for all Networks

<img src="https://imgur.com/M7CLdIN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Now Use pfsense as the default gateway for the Domain Controller

- Navigate to Control Panel >> Network and Internet >>  Network Connections

- Enter the following IP configuration

<img src="https://imgur.com/SOWEyj8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/Gq6zIzs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/E65oc3L.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/BRSy7qz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<h3>Windows 10 Desktop</h3>
This machine will be used as a user in the network. We would be connecting to the Domain created using the user account that was created on Active Directory.

- Add a network adapter as VMnet3
<img src="https://imgur.com/2Xx7dHb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Install Windows 10 using the default configuration

<img src="https://imgur.com/85p1BXM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Navigate to Network Adapter settings
- Right-click on Ethernet0 and select "properties"
- Select IPV4
- Add an IP Address(192.168.2.21) and Use 192.168.2.1 as the default gateway
- Use 192.168.2.10(VictimsNetwork) as the DNS Server

<img src="https://imgur.com/kWMOAJa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Add Windows to Domain
- Search “domain” and select Access work or school
- Select Connect >> Join this device to local Active Directory Domain
- Enter your domain name.local (homelab.local)
- You will be prompted to login as the domain controller administrator
- Complete the process by clicking next and restart  the windows machine

<img src="https://imgur.com/XBFsRUk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/ncXchqf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/Es5SDQR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Go back to the Domain controller and 
- User has been added on Windows Server

<img src="https://imgur.com/6htTGUE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<h3>Splunk</h3>
Splunk is one of the most widely used SIEMs in the Cybersecurity industry. Splunk essentially aggregates logs and datasets from various data sources and correlates all that information for easy searching, parsing & indexing.

- Install Ubuntu Server
- Add network adapter VMnet6
- Install the server using all the default settings and create a profile

<img src="https://imgur.com/gFMnhHX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/GaBUwNO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<b>Note: During the installation, you’ll be prompted to remove the CD(ISO) remove it and then reboot the VM.</b>

- After the VM has rebooted, your sign-in screen should look something similar to this.

<img src="https://imgur.com/XOnJSPo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<b>For the Splunk server, you have one of two options
- Accessing it with the AnalystVM using SSH
- Installing a GUI (Ubuntu Desktop) on the Ubuntu Server </b>

For this homelab, I will be accessing Splunk with the AnalystVM using SSH
- Install OpenSSH on the server by following the command below

<img src="https://imgur.com/R1HHYfS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Check for the status of SSH with the “sudo systemctl status ssh” command
- Confirm the IP address, this would be used to log in remotely and securely on the AnalystVM

<img src="https://imgur.com/SpV4Wck.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/fHmQF6o.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/6wCpBw8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Visit Splunk website and get the download link for Linux
- Install Splunk 
- Change the directory to where the configuration file is which should be the “/bin” folder
- Start Splunk using the “./splunk start” command
- Go to the web browser and log in using the Splunk IP address

<img src="https://imgur.com/2TLAcnG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/GFUQlLj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/KyEJj2m.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br>
<b>Installing Universal Forwarder</b>
<br/>

To log the activities on endpoints, Splunk uses a mechanism called the universal forwarder. The universal forward can be installed on Windows, *nix & mac agents to forward logs to your Splunk instance.

- Set up “Receiving” on your Splunk server
- Navigate to Settings >> Forwarding and Receiving >> New Receiving Port
- Enter port 9997 and save
- Navigate to Settings >> Indexes >> New index
- Name the index “wineventlog” and save

<img src="https://imgur.com/tcoMw0C.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/hNa92vL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/BpW2Fs3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/kK0MpLw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/CXmxqp6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/moONJDZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/NOm9e1b.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- On your Windows Server, Download the Universal Forwarder
- Now install the forwarder
- Accept the License Agreement & click Next
- Create a preferred username and password
- Enter the IP Address of your Splunk server and the default ports as prompted (8089 & 9997)
- Install
- Navigate back to your Splunk Instance >> Settings >> Add Data
- Select "Forward"
- Select the Domain Controller (Windows Server) >> Enter a Server Class Name e.g “Domain Controller” >> Next
- Select Local Events Logs and choose your desired event logs >> Next
- Select “wineventlog” as the index >> Review >> Submit

<img src="https://imgur.com/saH5uKi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/q2k4ABv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/pbxlGsY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/OqTexEX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/L8KvWDc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
