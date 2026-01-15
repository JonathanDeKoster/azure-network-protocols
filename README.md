<p align="center">
  <img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

# Azure Virtual Machines: Network Security Groups and Traffic Analysis

**Project Overview**

Hands-on Azure lab exploring virtual machine deployment, network security, and traffic analysis. Demonstrates practical experience configuring Azure VMs, observing network traffic, and applying network security rules.

**Objective**

Gain hands-on experience with Azure network protocols, virtual machine management, and network security controls relevant to entry-level IT and cloud support roles.

**What This Lab Covers**

- Creating and configuring Azure virtual machines (Windows & Ubuntu)
- Monitoring and analyzing network traffic using Wireshark
- Applying and testing Network Security Group (NSG) rules to control VM communication
- Understanding network protocols including ICMP, SSH, DHCP, DNS, and RDP
- Using PowerShell and Remote Desktop for VM management
---

## Environments and Technologies Used

- Microsoft Azure (Virtual Machines, Resource Groups, NSGs)  
- Windows 10 VM (21H2)  
- Ubuntu Server 20.04 VM  
- Remote Desktop (RDP)  
- PowerShell / CLI Tools  
- Wireshark  
- Network Protocols: ICMP, SSH, DHCP, DNS, RDP  

---

## Lab Objectives

- Build and configure VMs in Azure  
- Capture and analyze ICMP, SSH, DHCP, DNS, and RDP traffic  
- Modify NSG rules and observe traffic changes  
- Understand how Azure network security controls affect communication  

---

## High-Level Steps

1. **Part 1 – Virtual Machine Creation**  
2. **Part 2 – Observing ICMP Traffic**  
3. **Part 3 – Firewall Configuration & Traffic Analysis**  

---

## Part 1: Creating Virtual Machines

**Steps:**  
- Create a Resource Group in Azure  
- Deploy a Windows 10 VM  
- Allow Azure to create a new virtual network and subnet  
- Deploy an Ubuntu VM in the *same* Resource Group and VNet  
- Use username/password authentication  
- Confirm both VMs are located in the same subnet  

**Why:**  
Both VMs must share the same network space so we can observe direct traffic between them.

<details>
  <summary>View Screenshots</summary>

<img width="1230" height="772" src="https://github.com/user-attachments/assets/6102208f-d2ba-4d26-8821-0563b6536e5b" />
<img width="1217" height="757" src="https://github.com/user-attachments/assets/620f460d-7bce-410c-8b66-397f8c921825" />
<img width="1599" height="763" src="https://github.com/user-attachments/assets/ca4e88e1-6402-47db-b3f1-7e377b6546b5" />
<img width="1600" height="772" src="https://github.com/user-attachments/assets/6e169989-6d24-4316-b0e1-9fd9668b1d19" />
<img width="1600" height="771" src="https://github.com/user-attachments/assets/948fd882-2043-452d-96e1-a3dad4c042a5" />

</details>
---

## Part 2: Observing ICMP Traffic

**Steps:**  
- RDP into the Windows VM  
- Install and open Wireshark  
- Start a packet capture and filter for **ICMP**  
- Ping the Ubuntu VM using its private IP  
- Ping a public website (e.g., `google.com`)  
- Observe ICMP echo requests/replies in Wireshark  

**Why:**  
ICMP helps visualize connectivity between VMs and the Internet.

<details>
  <summary>View Screenshots</summary>

<img width="587" height="386" src="https://github.com/user-attachments/assets/02e99167-196b-4ce7-9eb0-770e1df53e2e" />
<img width="1553" height="842" src="https://github.com/user-attachments/assets/776c0a09-b0a6-490b-87e6-b488de7b7583" />
<img width="1552" height="825" src="https://github.com/user-attachments/assets/25075328-1836-4de5-ba45-5c76ae39b042" />
<img width="1535" height="824" src="https://github.com/user-attachments/assets/1fec5cfd-8712-4950-b8e3-05dd060e5b68" />
<img width="1544" height="822" src="https://github.com/user-attachments/assets/42895b99-ba06-4a5e-a1b7-ba4e1ef2136" />
<img width="1539" height="821" src="https://github.com/user-attachments/assets/2752e2fd-9bb1-46fb-97b1-b981b71444a8" />
<img width="1600" height="774" src="https://github.com/user-attachments/assets/4d89393c-9f85-4769-aadd-ea36600d0c86" />
<img width="1544" height="824" src="https://github.com/user-attachments/assets/05685b99-ff3c-460a-8cd5-6f99ae47ed37" />

</details>

---

## Part 3: Firewall Configuration & Traffic Analysis

### **ICMP Traffic**
- Start a continuous ping from Windows to Ubuntu  
- Disable inbound ICMP in the Ubuntu VM’s NSG  
- Observe ping failures in Wireshark  
- Re-enable ICMP to restore connectivity

<details>
  <summary>View Screenshots</summary>

<img width="1544" height="826" src="https://github.com/user-attachments/assets/46c0bfa2-937e-41d4-8fa6-b65b3e4e9933" />
<img width="1600" height="773" src="https://github.com/user-attachments/assets/40f067d0-d6a3-41f2-8771-b32fe0f6643a" />
<img width="1538" height="823" src="https://github.com/user-attachments/assets/07d06a99-c47c-4f38-ba8f-75b86ee02d8d" />
<img width="1554" height="842" src="https://github.com/user-attachments/assets/b45e6c1b-fa33-44ae-80fa-cc53e1a93947" />
<img width="1536" height="825" src="https://github.com/user-attachments/assets/f046086e-975b-4539-a4b3-daae5811c21a" />
<img width="1557" height="841" src="https://github.com/user-attachments/assets/99b40677-4715-4cc5-a458-b57e6856b901" />

</details>

---

### **SSH Traffic**
**Steps:**  
- Filter for **SSH** in Wireshark  
- SSH to Ubuntu from Windows PowerShell: ssh labuser@Ubuntu-Private-IP
- Observe authentication and session traffic  
- Exit session  

<details>
  <summary>View Screenshots</summary>

<img width="1545" height="824" src="https://github.com/user-attachments/assets/5ea32c6e-d4c8-44f0-ac94-46da51f30925" />
<img width="1467" height="841" src="https://github.com/user-attachments/assets/7f14d33c-1586-40af-8b91-c016277a9e91" />

</details>
---

### **DHCP Traffic**

**Steps:**  
- Filter for **DHCP** in Wireshark  
- Run: `ipconfig /renew`  
- Observe DHCP Discover/Offer/Request/Ack  
- Create a `dhcp.bat` script containing:
  ipconfig /release
  ipconfig /renew
- Execute the script and monitor DHCP packets  

<details>
<summary>View Screenshots</summary>

<img width="1467" height="825" src="https://github.com/user-attachments/assets/800c8f57-e76d-4ef5-87be-84c010ef0a86" />
<img width="1556" height="844" src="https://github.com/user-attachments/assets/3875ceea-b998-4fca-99f6-c48a983d7817" />
<img width="1542" height="831" src="https://github.com/user-attachments/assets/9eb3ab50-29d5-4714-9e07-1c5e39bb3891" />
<img width="1555" height="835" src="https://github.com/user-attachments/assets/256f8964-ac57-4162-b41a-0eaca307a54e" />
<img width="1537" height="822" src="https://github.com/user-attachments/assets/ec310f47-63da-42c9-b57f-54a7787aac02" />
<img width="1553" height="839" src="https://github.com/user-attachments/assets/bf2329c6-0e6d-4c12-ac95-b7574d8294f0" />

</details>
---

### **DNS Traffic**

**Steps:**  
- Filter for **DNS** in Wireshark  
- Run:
   nslookup google.com
   nslookup disney.com
- Observe DNS queries and responses  

<details>
<summary>View Screenshots</summary>

<img width="1553" height="828" src="https://github.com/user-attachments/assets/3ce8fc14-9382-4230-9cf8-3c7f2ce64bf7" />
<img width="1559" height="824" src="https://github.com/user-attachments/assets/aecd03cd-66d9-45cc-9be9-6e46ec0fdfd1" />

</details>
---

### **RDP Traffic**

**Steps:**  
- Filter for **RDP** in Wireshark  
- Observe continuous two-way stream of packets  

**Why:**  
RDP continuously transmits display updates and user input, making it extremely “chatty.”

<details>
<summary>View Screenshots</summary>

<img width="1554" height="839" src="https://github.com/user-attachments/assets/e9d4ff30-9043-43c2-a8e5-93530a1b9e1f" />

</details>
---


