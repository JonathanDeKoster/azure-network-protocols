<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

# Azure Virtual Machines: Network Security Groups and Traffic Analysis

This tutorial demonstrates **observing network traffic** between Azure Virtual Machines using Wireshark and experimenting with **Network Security Groups (NSGs)**.  

---

## Video Demonstration

- [YouTube: Azure Virtual Machines, Wireshark, and NSGs](https://www.youtube.com)

---

## Environments and Technologies Used

- Microsoft Azure (Virtual Machines / Compute / NSGs)  
- Windows 10 VM (21H2)  
- Ubuntu Server 20.04 VM  
- Remote Desktop  
- PowerShell / Command-Line Tools  
- Wireshark (Protocol Analyzer)  
- Network Protocols: ICMP, SSH, DHCP, DNS, RDP  

---

## Lab Objectives

- Build and configure VMs in Azure  
- Observe ICMP, SSH, DHCP, DNS, and RDP traffic  
- Configure firewall rules via NSGs  
- Analyze traffic and connectivity behavior  
- Understand the impact of NSGs on VM communication  

---

## High-Level Steps

1. **Part 1 – VM Creation**  
2. **Part 2 – Observing ICMP Traffic**  
3. **Part 3 – Firewall Configuration & Traffic Analysis**  
4. **Cleanup**  

---

## Part 1: Creating Virtual Machines

**Steps:**  
- Create a Resource Group in Azure  
- Create a Windows 10 VM in the Resource Group  
- Allow Azure to create a new VNet and Subnet  
- Create an Ubuntu VM in the same Resource Group and VNet  
- Use Username/Password authentication for the Ubuntu VM  
- Ensure both VMs are in the same subnet  
- Keep both VMs for Part 2  

**Why:** Both VMs need to be on the same network for traffic observation and testing.  

**Screenshots:**  
![NA1](https://github.com/user-attachments/assets/054dcc26-30ac-4e03-8c1d-bc44efc1077e)  
![NA2](https://github.com/user-attachments/assets/bb8ba21a-ec4f-4992-9a0f-00210ce9d14c)  

---

## Part 2: Observing ICMP Traffic

**Steps:**  
- Remote Desktop into Windows VM  
- Install Wireshark  
- Start packet capture and filter **ICMP**  
- Ping Ubuntu VM by its private IP  
- Ping a public website (e.g., google.com)  
- Observe request and reply packets in Wireshark  

**Why:** Learn how ICMP traffic travels between VMs and to the Internet.  

**Screenshots:**  
![NA21](https://github.com/user-attachments/assets/d3fbaab5-0ed9-476c-9dfc-40a53944b418)  
![NA22](https://github.com/user-attachments/assets/3ede18d5-716a-4d4e-83ae-6484e19d5701)  

  

---

## Part 3: Firewall Configuration & Traffic Analysis

**ICMP Traffic**  
- Initiate continuous ping from Windows to Ubuntu VM  
- Disable inbound ICMP in Ubuntu NSG  
- Observe ping failures in Wireshark  
- Re-enable ICMP and verify connectivity  

**SSH Traffic**  
- Filter **SSH** in Wireshark  
- SSH from Windows VM to Ubuntu VM:  
  ```powershell
  ssh labuser@<Ubuntu-Private-IP>
**DHCP Traffic**
- Filter DHCP in Wireshark
- Renew IP on Windows VM
- Observe DHCP Traffic

**DNS Traffic**
-Filter DNS in Wireshark
- Use nslookup google.com or nslookup disney.com
- Observe DNS queries and responses

**RDP Traffic**
- Filter RDP in Wireshark
- Observe constant stream of traffic
- **Why**: RDP transmits a continuous display and input stream

- 
