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
Kali Linux will be used as an attack machine to propagate different forms of offensive actions against the Domain Controller and the other machines attached to it.


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
