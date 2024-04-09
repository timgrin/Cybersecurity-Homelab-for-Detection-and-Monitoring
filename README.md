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
<img src="https://imgur.com/nrxZXHg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
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
Interface assignment <br />
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

<h2>Security Onion</h2>
This will be the all-in-one IDS, Security Monitoring, and Log Management solution.

- Select Typical installation >> Click “Next”
- Installer disc image file >> SO ISO file path >> Click “Next”
- Choose “Linux”, “CentOS 7 64-Bit” and click “Next”.
- Specify the virtual machine name and click Next.
- Click “Customize Hardware” 
- Change memory to 4-32GB
- Add two Network Adapters and assign them Vmnet 4 & Vmnet 5 respectively
<img src="https://imgur.com/jDz2G4G.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
