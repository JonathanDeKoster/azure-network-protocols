<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

# Azure Virtual Machines: Network Security Groups and Traffic Analysis

This tutorial demonstrates **observing network traffic** between Azure Virtual Machines using Wireshark and experimenting with **Network Security Groups (NSGs)**.  


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
<img width="1230" height="772" alt="NA1" src="https://github.com/user-attachments/assets/6102208f-d2ba-4d26-8821-0563b6536e5b" />
<img width="1217" height="757" alt="NA2" src="https://github.com/user-attachments/assets/620f460d-7bce-410c-8b66-397f8c921825" />
<img width="1599" height="763" alt="NA3" src="https://github.com/user-attachments/assets/ca4e88e1-6402-47db-b3f1-7e377b6546b5" />
<img width="1600" height="772" alt="NA4" src="https://github.com/user-attachments/assets/6e169989-6d24-4316-b0e1-9fd9668b1d19" />
<img width="1600" height="771" alt="NA5" src="https://github.com/user-attachments/assets/948fd882-2043-452d-96e1-a3dad4c042a5" />

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
<img width="587" height="386" alt="NA21" src="https://github.com/user-attachments/assets/02e99167-196b-4ce7-9eb0-770e1df53e2e" />
<img width="1553" height="842" alt="NA22" src="https://github.com/user-attachments/assets/776c0a09-b0a6-490b-87e6-b488de7b7583" />
<img width="1552" height="825" alt="NA23" src="https://github.com/user-attachments/assets/25075328-1836-4de5-ba45-5c76ae39b042" />
<img width="1535" height="824" alt="NA24" src="https://github.com/user-attachments/assets/1fec5cfd-8712-4950-b8e3-05dd060e5b68" />
<img width="1544" height="822" alt="NA25" src="https://github.com/user-attachments/assets/42895b99-ba06-4a5e-a1b7-ba4ee1ef2136" />
<img width="1539" height="821" alt="NA26" src="https://github.com/user-attachments/assets/2752e2fd-9bb1-46fb-97b1-b981b71444a8" />
<img width="1600" height="774" alt="NA27" src="https://github.com/user-attachments/assets/4d89393c-9f85-4769-aadd-ea36600d0c86" />
<img width="1544" height="824" alt="NA28" src="https://github.com/user-attachments/assets/05685b99-ff3c-460a-8cd5-6f99ae47ed37" />

  

---

## Part 3: Firewall Configuration & Traffic Analysis

**ICMP Traffic**  
- Initiate continuous ping from Windows to Ubuntu VM  
- Disable inbound ICMP in Ubuntu NSG  
- Observe ping failures in Wireshark  
- Re-enable ICMP and verify connectivity  

<img width="1544" height="826" alt="NA210" src="https://github.com/user-attachments/assets/46c0bfa2-937e-41d4-8fa6-b65b3e4e9933" />
<img width="1600" height="773" alt="NA211" src="https://github.com/user-attachments/assets/40f067d0-d6a3-41f2-8771-b32fe0f6643a" />
<img width="1538" height="823" alt="NA212" src="https://github.com/user-attachments/assets/07d06a99-c47c-4f38-ba8f-75b86ee02d8d" />
<img width="1554" height="842" alt="NA213" src="https://github.com/user-attachments/assets/b45e6c1b-fa33-44ae-80fa-cc53e1a93947" />
<img width="1536" height="825" alt="NA214" src="https://github.com/user-attachments/assets/f046086e-975b-4539-a4b3-daae5811c21a" />
<img width="1557" height="841" alt="NA215" src="https://github.com/user-attachments/assets/99b40677-4715-4cc5-a458-b57e6856b901" />


**SSH Traffic**  
- Filter **SSH** in Wireshark
- SSH from Windows VM to Ubuntu VM in Powershell:  
  ssh labuser@<Ubuntu-Private-IP>

  
<img width="1545" height="824" alt="NA32" src="https://github.com/user-attachments/assets/5ea32c6e-d4c8-44f0-ac94-46da51f30925" />
<img width="1467" height="841" alt="NA33" src="https://github.com/user-attachments/assets/7f14d33c-1586-40af-8b91-c016277a9e91" />

  
**DHCP Traffic**
- Filter DHCP in Wireshark
- Renew IP on Windows VM
- Observe DHCP Traffic
  no dhcp traffic
<img width="1467" height="825" alt="NA34" src="https://github.com/user-attachments/assets/800c8f57-e76d-4ef5-87be-84c010ef0a86" />
run ipconfig/renew
one communication
<img width="1556" height="844" alt="NA35" src="https://github.com/user-attachments/assets/3875ceea-b998-4fca-99f6-c48a983d7817" />
Create file dhcp.bat containing ipconfig /release and ipconfig / renew
<img width="1542" height="831" alt="NA36" src="https://github.com/user-attachments/assets/9eb3ab50-29d5-4714-9e07-1c5e39bb3891" />
find dhcp.bat in powershell
<img width="1555" height="835" alt="NA37" src="https://github.com/user-attachments/assets/256f8964-ac57-4162-b41a-0eaca307a54e" />
find dhcp.bat in command prompt
<img width="1537" height="822" alt="NA38" src="https://github.com/user-attachments/assets/ec310f47-63da-42c9-b57f-54a7787aac02" />
execute dhcp.bat in powershell, observe in wireshark
<img width="1553" height="839" alt="NA39" src="https://github.com/user-attachments/assets/bf2329c6-0e6d-4c12-ac95-b7574d8294f0" />


**DNS Traffic**
-Filter DNS in Wireshark
- Use nslookup google.com or nslookup disney.com
- Observe DNS queries and responses

**RDP Traffic**
- Filter RDP in Wireshark
- Observe constant stream of traffic
- **Why**: RDP transmits a continuous display and input stream

- 
