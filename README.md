# <p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04


<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/6KPh73h.png"
</p>
<p>
Created a Resourse Group inside Microsoft Azure (Step-1)
</p>
<br />

<p>
<img src="https://i.imgur.com/DKO8aDN.png"
</p>
<p>
Made a new Virtual Network for resourse group and VMs we will create (Step-2)
</p>
<br />

<p>
<img src="https://i.imgur.com/97BM2yE.png"
</p>
<p>
Then created two VMs one running windows 10 pro and the other running Ubuntu 22 (Step-3)
</p>
<br />

<p>
<img src="https://i.imgur.com/7oDY9LV.png"
</p>
<p>
Installed wireshark on windows-vm (Step-4)
</p>
<br />

<p>
<img src="https://i.imgur.com/1d1u9sw.png"
</p>
<p>
Observe packets (IP packets) going through wireshark (VMs network traffic) (Step-5)
</p>
<br />

<p>
<img src="https://i.imgur.com/F2vcViU.png"
</p>
<p>
Filtered wireshark to only pick up ICMP (or ping traffic) only (Step-6)
</p>
<br />

<p>
<img src="https://i.imgur.com/xk2VwoO.png"
</p>
<p>
From inside windows-vm we pinged linux vms private IP address to see we successfully got a reply and observed the ICMP traffic within wireshark (Step-7)
</p>
<br />

<p>
<img src="https://i.imgur.com/Vjuca8N.png"
</p>
<p>
Looked into wireshark at the source and destination IP addresses (MAC addresses in pic) and noticed they matched with our VMs (step-8)
</p>
<br />

<p>
<img src="https://i.imgur.com/GWtnnKm.png"
</p>
<p>
Inspected the payload (random letters) and how it matched for both windows and linux VMs (data sent and data recieved request-reply)) (Step-9)
</p>
<br />

<p>
<img src="https://i.imgur.com/sOnfAOU.png"
</p>
<p>
Initiated a non-stop ping (or perpetual ping) from windows VM to linux VM (Step-10)
</p>
<br />

<p>
<img src="https://i.imgur.com/8ZW3ljS.png"
</p>
<p>
Created a new inbound security rule for linux vm denying all ICMP traffic (Step-11)
</p>
<br />

<p>
<img src="https://i.imgur.com/eyFDvK5.png"
</p>
<p>
Back in windows-vm observed that ICMP traffic from linux-vm timed out (linux VM started to ignore ICMP replys) (Step-12)
</p>
<br />

<p>
<img src="https://i.imgur.com/kUhH10l.png"
</p>
<p>
Deleted firewall rule and observed requests got picked back up again (Step-13)
</p>
<br />

<p>
<img src="https://i.imgur.com/HgrSkY7.png"
</p>
<p>
Connected to linux machine inside windows vm using ssh within powershell (with username and linux vm private IP address) and obeserved SSH traffic (Step-14)
</p>
<br />

<p>
<img src="https://i.imgur.com/7m7jtVd.png"
</p>
<p>
Notice how prompt changed because we were now connected to linux vm (Step-15)
</p>
<br />

<p>
<img src="https://i.imgur.com/XDRE4Gt.png"
</p>
<p>
Obeserved the hostname (says linux VM while using windows) (Step-16)
</p>
<br />

<p>
<img src="https://i.imgur.com/7PvQsHS.png"
</p>
<p>
Because we were using SSH we noticed that packets were encrypted (not telnet or cleartext) (Step-17)
</p>
<br />

<p>
<img src="https://i.imgur.com/ejjXNZZ.png"
</p>
<p>
Observed SSH uses TCP port 22 to communicate (can use tcp.port==22 to filter traffic as well) (Step-18)
</p>
<br />

<p>
<img src="https://i.imgur.com/usmOZgr.png"
</p>
<p>
Next we dropped the SSH connection by typing exit (Step-19)
</p>
<br />

<p>
<img src="https://i.imgur.com/xA8QvpJ.png"
</p>
<p>
Looked at the RST (reset package) that was sent which just kills the connection (Step-20)
</p>
<br />

<p>
<img src="https://i.imgur.com/jS1Zvej.png"
</p>
<p>
Renewed Ip address and filtered for DHCP traffic only (Step-21)
</p>
<br />

<p>
<img src="https://i.imgur.com/xilYttj.png"
</p>
<p>
Again observed new DHCP traffic (Step-22)
</p>
<br />

<p>
<img src="https://i.imgur.com/LTI5uyh.png"
</p>
<p>
Looked at destination IP address (255.255.etc) which means broadcast (Step-23)
</p>
<br />

<p>
<img src="https://i.imgur.com/E1yKPcg.png"
</p>
<p>
Lastly observed DNS and RDP traffic and cleaned up the lab (Step-24)
</p>
