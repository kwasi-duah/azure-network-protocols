# Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines using Wireshark

This tutorial will guide you step-by-step in observing network traffic to and from Azure Virtual Machines using Wireshark and experimenting with Network Security Groups (NSGs). Let's get started!

## Environments and Technologies Used

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Network Protocols (ICMP, SSH, DHCP, DNS, RDP)
- Wireshark (Protocol Analyzer)

## Operating Systems Used

- Windows 10 (21H2)
- Ubuntu Server 20.04

## High-Level Steps

1. Create a Resource Group
2. Create a Virtual Machine
3. Observe ICMP Traffic
4. Observe SSH Traffic
5. Observe DHCP Traffic
6. Observe DNS Traffic
7. Observe RDP Traffic

## Actions and Observations

### 1. Set Up Your Virtual Environment

Create a Resource Group in your Azure subscription.

![Resource Group](https://i.imgur.com/dOAeXqs.png)

Create a Windows Virtual Machine in the same Resource Group. Allow it to create a new Virtual Network (VNet) and Subnet.

![Windows VM](https://i.imgur.com/PHOwjLh.png)

Next, create an Ubuntu Virtual Machine, again using the same Resource Group and allowing it to create a new VNet and Subnet.

![Ubuntu VM](https://i.imgur.com/N5zwQUH.png)

Check your Virtual Network in Azure Network Watcher:

![Network Watcher](https://i.imgur.com/Pn02GXF.png)

### 2. Observe ICMP Traffic

Remote into your Windows 10 Virtual Machine, install Wireshark, and filter for ICMP traffic.

![Remote Desktop](https://i.imgur.com/0BsfNiS.jpg)

Ping the private IP of your Ubuntu VM from the Windows VM and observe the traffic in Wireshark:

![ICMP traffic](https://i.imgur.com/3h9QSEY.png)

Now, ping a public website like www.google.com and observe the traffic:

![ICMP traffic public](https://i.imgur.com/YduMvc7.png)

Disable incoming ICMP traffic in the Network Security Group (NSG) of your Ubuntu VM and observe the impact in Wireshark:

![ICMP traffic blocked](https://i.imgur.com/NjuUANI.png)

Re-enable ICMP traffic and observe the pings working again:

![ICMP traffic re-enabled](https://i.imgur.com/nZbl2sA.png)

### 3. Observe SSH Traffic

Filter for SSH traffic in Wireshark. SSH into your Ubuntu VM from the Windows VM using its private IP address. Run commands and observe the traffic:

![SSH traffic](https://i.imgur.com/6YEDJKu.png)

### 4. Observe DHCP Traffic

Filter for DHCP traffic in Wireshark. Issue a new IP address for your Windows VM using `ipconfig /renew` and observe the traffic:

![DHCP traffic](https://i.imgur.com/mKyAHFr.png)

### 5. Observe DNS Traffic

Filter for DNS traffic in Wireshark. Use `nslookup` to find the IP addresses of websites like google.com:

![DNS traffic](https://i.imgur.com/mYZ8CAK.png)

### 6. Observe RDP Traffic

Filter for RDP traffic in Wireshark using `tcp.port==3389`. Observe the constant traffic due to the live stream of data:

![RDP traffic](https://i.imgur.com/hNlhTVp.png)

### 7. Clean Up

Close your Remote Desktop connection, delete the Resource Group, and verify its deletion to avoid unnecessary charges.

That's it! You've successfully observed various network traffic and experimented with NSGs in Azure!
