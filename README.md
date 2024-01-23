<p align="center">
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

<h2>High-Level Steps</h2>

- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DCHP Traffic
- Observe DNS Traffic
- Observe RDP Traffic

<h2>Actions and Observations</h2>

Observing ICMP Traffic
----------------------
![image](https://github.com/git-oscas/azure-network-protocols/assets/156957308/9002ad3f-418b-46ac-877a-a648508a3935)

Within VM-1 (Windows 10), install/open "WireShark" to filter for ICMP traffic only, and retreive the private IP address (10.0.0.5) of VM-2 (Ubuntu) and attempt to ping it from within VM-1 (Windows 10)

![image](https://github.com/git-oscas/azure-network-protocols/assets/156957308/02ad27d2-6365-44cf-a5fd-91c4d68fa21f)

Initiate a perpetual ping from VM-1 (Windows 10) to VM-2 (Ubuntu)

![image](https://github.com/git-oscas/azure-network-protocols/assets/156957308/1de1ad0b-dacb-4e0a-9ef2-009591c1fb7f)

Within the Azure Portal, open the Network Security Group (NSG) VM-2 (Ubuntu) is using and disable inbound ICMP traffic

![image](https://github.com/git-oscas/azure-network-protocols/assets/156957308/ce22fedb-69a3-4251-be16-dc6c51a7c938)

In VM-1, observe the ping no longer receives replies

![image](https://github.com/git-oscas/azure-network-protocols/assets/156957308/d5953757-36d0-4dcc-87a5-a0d0b670bca2)

Re-enable ICMP traffic within VM-2 NSG

![image](https://github.com/git-oscas/azure-network-protocols/assets/156957308/0e53d213-5286-445e-aab6-c8d7b8d67f37)

Back on VM-1 in WireShark, the ping now receives replies from VM-2

Observing SSH Traffic
---------------------
Filter for SSH traffic within WireShark

![image](https://github.com/git-oscas/azure-network-protocols/assets/156957308/ce7d0ec6-9320-490f-8192-b32846471833)

From VM-1 (Windows 10), "SSH into" VM-2 (Ubuntu) via its private IP address (10.0.0.5)

![image](https://github.com/git-oscas/azure-network-protocols/assets/156957308/85100e31-1f3b-496c-8b05-4238ba432ccc)

Anything typed within the command line will now traffic spam in WireShark

Observing DCHP Traffic
----------------------
Filter for DHCP traffic within WireShark

![image](https://github.com/git-oscas/azure-network-protocols/assets/156957308/d84d6952-10a1-4a3c-a6b4-b8444eb56fb2)

Back in VM-1 (Windows 10), issue the VM a new IP address from the command line and observe the DHCP traffic in WireShark

Observing DNS Traffic
---------------------
Filter for DNS traffic within WireShark

![image](https://github.com/git-oscas/azure-network-protocols/assets/156957308/70684a97-fe54-497b-8825-1902d6116365)

From VM-1 (Windows 10) within a command line, use nslookup to see what googles' IP addresses are and observe the traffic within WireShark

Observing RDP Traffic
---------------------
Filter for RDP traffic within WireShark

![image](https://github.com/git-oscas/azure-network-protocols/assets/156957308/e2350079-a6ec-4469-9d29-8d52ae55285b)

Observe the non-stop traffic spam when filtering for RDP, this is because the connection from one comupter to another is active, therefore traffic is constantly being transmitted
