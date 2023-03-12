<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Actions and Observations</h2>

<p>
Welcome to my tutorial on Network Security Groups and Inspecting Network Protocols. First you will need to create two VMs on Azure. One machine will be a Linux machine and the other will be a Windows 10 machine. Both will have two cpus and they must be on the same VNET. Once that is done go on the Windows machine and download Wireshark. I will attatch a link to the wireshark download. https://www.wireshark.org/download.html Once installed open Wireshark and filter for ICMP Traffic only. ICMP is a network layer protocol that relays messages concerning network connection issues. Ping uses this protocol, ping tests connectivity between hosts. When we filter wirehsark to only capture ICMP packets and ping the private IP address of our linux machine we can visually see the packets on wireshark. 
</p>
<br />

<p>
<img src="https://i.imgur.com/IIUShxp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In the image, we can inspect each individual packet and see the actual data that is being sent in each ping.
</p>
<br />

<p>
<img src="https://i.imgur.com/5vXO75R.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><br />
<img src="https://i.imgur.com/Asl80tN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><br />
</p>
<p>
Use the ping -t command to ping the Linux computer continuously. While the Windows computer is pinging the Linux machine, we will go to the Linux machine and prevent inbound ICMP traffic on its firewall. This will keep pinging the machine until we decide to halt it. When we do that, the Linux computer will no longer send us repeat responses. On the Linux computer, a new Network Security Group will be created and configured to prevent ICMP. By enabling ICMP on the Linux Network Security Groups tab in Azure, we can enable the traffic. 
</p>
<br />

<p>
<img src="https://i.imgur.com/zteR41r.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><br />
</p>
<p>
Next, we'll SSH into the Linux server from our Windows computer. SSH only provides access to the machine's command line; it lacks a GUI. Wireshark's filter will be configured to only depict and record SSH messages.
</p>

<p>
<img src="https://i.imgur.com/vU8fpQf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><br />
</p>
<p>
Wireshark will now be used to check for DHCP. The Dynamic Host Configuration Protocol (DHCP) uses port 67 and 68 to assign IP addresses. We will use the command "ipconfig /renew" to obtain a new IP address and DHCP data will be captured by wireshark once we have entered the instruction.
</p>

<p>
<img src="https://i.imgur.com/VMcwmsO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Wireshark will be configured to filter DNS traffic. By entering the command "nslookup www.google.com," which basically queries our DNS server for Google's IP address, we will start DNS traffic.
</p>

<br />
<img src="https://i.imgur.com/VxXGv6X.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
