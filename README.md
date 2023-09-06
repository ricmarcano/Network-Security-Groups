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

<h2>The Set-Up</h2>

Within Azure, I created two VMs within the same virtual network to ensure that they are able to communicate with each other. One VM will have Windows 10 Pro while the other uses Ubuntu. The Windows VM will connect to the other via the command line/PowerShell. 

<h2>Actions and Observations</h2>

Connect to the Windows VM through Remote Desktop using its public IP address and then install Wireshark to begin inspecting the traffic.
