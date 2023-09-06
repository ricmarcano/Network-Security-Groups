<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Inspecting Traffic Between Azure Virtual Machines</h1>
In this lab, we will observe different kinds of network traffic to and from Azure virtual machines with Wireshark as well as experiment with network security groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop Connection
- Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 Pro (21H2)
- Ubuntu Server 20.04

<h2>Set Up</h2>

Within Azure, I created two VMs within the same virtual network to ensure that they are able to communicate with each other. One VM will have Windows 10 Pro while the other uses Ubuntu. The Windows VM will connect to the other via the command line/PowerShell. 

<h2>Actions and Observations</h2>

Connect to the Windows VM through Remote Desktop using its public IP address and then install Wireshark to begin inspecting the traffic.

![image](https://github.com/ricmarcano/Network-Security-Groups/assets/141169092/c7e383bc-4c3c-48a5-9564-4630c2ac735c)

In Wireshark, I applied a filter for ICMP (Internet Control Message Protocol) traffic. Then, I launched PowerShell to run the "ping" command, which utilizes ICMP for network troubleshooting purposes. I used "ping" to check connectivity with the Ubuntu VM using its private IP address and with google.com. Afterward, I conducted a continuous ping to the Ubuntu VM to observe the behavior of network security groups. I initiated the continuous ping using the command: "ping -t (IP address)."

![image](https://github.com/ricmarcano/Network-Security-Groups/assets/141169092/ea06154c-9c19-4276-a7df-c6bde7adf75f)

Inside the Azure portal, I accessed the networking configuration for the Ubuntu VM and inserted an inbound security rule to deny ICMP traffic. I ensured that the rule's priority was set higher than SSH (300) to guarantee it takes precedence.

![Screenshot 2023-09-06 at 11 49 35 AM](https://github.com/ricmarcano/Network-Security-Groups/assets/141169092/d726db19-df93-417d-8ba5-d5c65d3f77e2)

Upon returning to the Windows VM, I observed that ICMP traffic was blocked due to the newly implemented inbound security rule. Once I modified the rule to allow traffic again, the continuous ping no longer experienced timeouts and functioned normally.

![image](https://github.com/ricmarcano/Network-Security-Groups/assets/141169092/9342fe34-c274-4ace-ae78-7cc033e30d4b)
![image](https://github.com/ricmarcano/Network-Security-Groups/assets/141169092/2e9cd378-44c9-493b-9306-c6cfd73201a2)

I then focused on SSH traffic. I logged into the Ubuntu server using PowerShell's ssh command and filtered the traffic. Wireshark logged each of my commands while I was on the Ubuntu server.

![image](https://github.com/ricmarcano/Network-Security-Groups/assets/141169092/d7d1b973-8726-4d98-8b39-c17b96a2aac3)
![image](https://github.com/ricmarcano/Network-Security-Groups/assets/141169092/92525333-730d-427e-bf65-58dec3406c27)

After looking at SSH trafficit is now time to check for DHCP traffic. To see it in action, I attempted to get a new IP address for my VM using the "ipconfig /renew" command and Wireshark captured the resulting traffic. 

![image](https://github.com/ricmarcano/Network-Security-Groups/assets/141169092/8ae00dce-06c4-4852-8082-e644fa4bd3b2)

To examine DNS traffic, I applied the filter "udp.port == 53" and utilized the "nslookup" command. My goal was to observe the results of looking up disney.com it being highly popular website.

![image](https://github.com/ricmarcano/Network-Security-Groups/assets/141169092/1a2472d3-be7a-48bb-ade7-174ad0e90304)
![image](https://github.com/ricmarcano/Network-Security-Groups/assets/141169092/21fb0ae0-b860-40df-a576-f2511e0a7b02)

To conclude my lab session, I opted to monitor RDP traffic. I set up the Wireshark filter as "tcp.port == 3389." Since RDP continuously provides a live stream between computers (in my case, my computer connecting to the Azure-hosted VM), there is a constant flow of traffic.

![image](https://github.com/ricmarcano/Network-Security-Groups/assets/141169092/54544d6a-6370-4e38-9602-d27a8ea1732b)
