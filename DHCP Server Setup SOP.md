# Standard Operating Procedure (SOP): Setting Up a DHCP Server on Windows Server 2022

## 1. Introduction

### 1.1 Purpose
The purpose of this SOP is to guide system administrators in installing, configuring, and testing a DHCP Server on Windows Server 2022.

### 1.2 Scope
This SOP can be used by system administrators who manage network infrastructure in an organization through Windows Server 2022.

### 1.3 Prerequisites
Before starting the installation, ensure the following:
- Windows Server 2022 is installed and fully updated.
- Administrative privileges are available.
- The server is given a static IP address.
- The server is a member of the Active Directory domain (where relevant).

---

## 2. Approval and Authorization

#### **Written By:**
- **Sejalpreet Kaur** (System Administrator)  
- **Limusi A** (Network Specialist)  
- **Milan Singh** (IT Technician)  
- **Date**: 2025-03-31

---

## 3. Approval Table

| Approval Level | Name           | Title              | Date       | Comments   |
|----------------|----------------|--------------------|------------|------------|
| Author         | Sejal, Limusi, Milan | System Admin, Network Specialist, IT Technician | 2025-03-29 | Initial Draft |
| Approver       | Felix Liang    | Instructor | 2025-03-31 | Approved |

---

## 4. Reversion Info

| Version | Date       | Author           | Description                  |
|---------|------------|------------------|------------------------------|
| 1.0     | 2025-03-29 | Sejal, Limusi, Milan | Initial SOP Creation          |
| 1.1     | 2025-03-30 | Sejal, Limusi, Milan | Added Accountability Matrix   |

---

## 5. Network Topology
Below is a sample network topology for a DHCP deployment:
![image](https://github.com/user-attachments/assets/73896a2f-3b6d-496e-be5e-ed4cb71db0ee)


This setup ensures that all clients connected to the network via the switch receive IP addresses from the DHCP server.

## 6. IP Address Table

| Device        | IP Address       | Role             |
|---------------|------------------|------------------|
| Router        | 192.168.1.1      | Default Gateway  |
| DHCP Server   | 192.168.1.10     | IP Assignment    |
| Client 1      | 192.168.1.100    | Workstation      |
| Client 2      | 192.168.1.101    | Workstation      |
| Client 3      | 192.168.1.102    | Workstation      |

---

## 7. Step-by-Step Process

### Step 1: Install the DHCP Server Role

1. Open **Server Manager**.
2. Click **Manage** > **Add Roles and Features**.
![image](https://github.com/user-attachments/assets/4ca8ed13-f91e-4cd8-9da5-656f940263b8)
3. In the **Add Roles and Features Wizard**, click **Next**.
4. Select **Role-based or feature-based installation** and click **Next**. 
![image](https://github.com/user-attachments/assets/f8b435cd-9f48-41a6-a65d-7f1065de00e9)
5. Choose **Select a server from the server pool**, then click **Next**.
![image](https://github.com/user-attachments/assets/9452c877-6243-4a0a-a25e-7abd23ca3503)
6.Select **DHCP Server** and click **Next**
![image](https://github.com/user-attachments/assets/f524cf13-2f35-4eb1-93f3-b2d5cb4211d2)
7. Click **Add Features** when prompted.
8. Click **Next** until you reach the **Install** button, then click **Install**.
9. Wait for the installation to complete and click **Close**.
![image](https://github.com/user-attachments/assets/90cfef4f-b490-4024-b1f9-06239946110b)

---

### Step 2: Create a DHCP Scope

1. In the **DHCP Console**, right-click **IPv4**, then select **New Scope**.
![image](https://github.com/user-attachments/assets/0e745890-36e4-4d1c-9a7a-ba38c9a5b86f)
![image](https://github.com/user-attachments/assets/2b1e41f3-976c-41a2-8250-b5e57972aef3)
2. Enter a **Scope Name** (e.g., `Office DHCP Scope`) and click **Next**.
![image](https://github.com/user-attachments/assets/0b1dd419-2ad5-4608-abb7-8fd22491c397)
3. Define the **IP Address Range**:
   - Start IP Address: `192.168.1.100`
   - End IP Address: `192.168.1.200`
   - Click **Next**.
![image](https://github.com/user-attachments/assets/922cce1c-4c52-4c56-bcf2-880df97b426b)
4. Define an **Exclusion Range** (e.g., `192.168.1.150 to 192.168.1.160`) and click **Next**.
![image](https://github.com/user-attachments/assets/bf631221-e7a2-4c89-bb5f-34cd999e6915)
5. Set the **Lease Duration** (default: `8 days`), then click **Next**.
6. Choose **Yes, I want to configure these options now** and click **Next**.
![image](https://github.com/user-attachments/assets/5bbab290-e3c9-495d-9d3a-5ed7a7b71cd0)

---

### Step 3: Configure DHCP Scope Options

1. **Default Gateway**: Enter the router’s IP (e.g., `192.168.1.1`), then click **Next**.
![image](https://github.com/user-attachments/assets/7049396c-2a2e-4e40-9a88-90930e7cd1bd)
2. **DNS Server**:
   - Enter Preferred DNS (e.g., `8.8.8.8` for Google DNS).
   - Enter Alternate DNS (e.g., `8.8.4.4`).
   - Click **Next**.
4. Click **Next** and **Finish**.
   ![image](https://github.com/user-attachments/assets/6697c237-ca8a-493f-ab6c-21de940de811)

---

### Step 4: Authorize and Activate the DHCP Server

1. In **DHCP Manager**, right-click the server name and select **Authorize**.
2. Wait a few moments, then right-click the server and select **Refresh**.
3. Verify that the **green checkmark** appears, indicating activation.
![image](https://github.com/user-attachments/assets/bdc42a8a-36d5-4bd5-9502-eb5bf1ee5347)

---

### Step 5: Configure DHCP Failover (Optional)

1. Open **DHCP Manager** and right-click the **IPv4** node.
2. Select **Configure Failover**.
3. Click **Next**, then select the scope(s) to enable failover for and click **Next**.
4. Choose **Load Balance** or **Hot Standby** mode.
5. Enter the partner server’s IP or hostname and click **Next**.
6. Configure failover settings, then click **Finish**.
7. Verify replication on the partner DHCP server.

---

### Step 6: Verify DHCP Server Functionality

1. On a client machine, open **Command Prompt** and type:
   ```sh
   ipconfig /release
   ipconfig /renew

---

### Step 8: Troubleshooting

1. Common Issues & Solutions

| Issue                              | Possible Cause                    | Solution |
|------------------------------------|----------------------------------|----------|
| Clients not receiving IP addresses | Scope not activated or authorized | Verify DHCP Server is authorized and scope is active |
| Incorrect IP assignment            | Overlapping IP ranges             | Check exclusion ranges and correct the scope |
| Connectivity issues                | Incorrect gateway or DNS settings | Verify and correct default gateway and DNS settings |
| DHCP Server not starting           | Service not running               | Restart the DHCP service via `services.msc` |
| DHCP database corruption           | Improper shutdown                 | Restore from backup using `netsh dhcp server import` |

---

## Step 9: Accountability Matrix

| Task                            | Responsible Person       | Due Date    |
|---------------------------------|-------------------------|------------|
| Install DHCP Server Role        | Sejal, Limusi, Milan    | 2025-03-31 |
| Create DHCP Scope               | Sejal, Limusi, Milan    | 2025-03-31 |
| Configure DHCP Options          | Sejal, Limusi, Milan    | 2025-04-01 |
| Test DHCP Server Functionality  | Sejal, Limusi, Milan    | 2025-04-02 |

---

## Step 10: Revision History

| Version | Date       | Author               | Description                          |
|---------|-----------|----------------------|--------------------------------------|
| 1.0     | 2025-03-29 | Sejal, Limusi, Milan | Initial document creation           |
| 1.1     | 2025-03-30 | Sejal, Limusi, Milan | Added accountability matrix, visuals |
| 1.2     | 2025-04-01 | Sejal, Limusi, Milan | Updated troubleshooting section      |



    






