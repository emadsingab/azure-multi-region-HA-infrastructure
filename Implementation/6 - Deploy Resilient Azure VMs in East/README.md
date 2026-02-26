# 6. Deploy Resilient Azure VMs in East US 🖥️

## 🎯 Section Goal
Mirror the compute infrastructure deployed in the West region by provisioning highly available Windows Virtual Machines in the East US region. This establishes the foundational compute layer for multi-region redundancy and geo-routing.

---

## 🚀 Implementation Steps

### Task 1: Provisioning `EAST01` and Availability Set
To ensure identical architecture across regions, the exact same provisioning standards were applied to the East US region:

1. **Create Availability Set:** Deployed a new availability set named `AvailSet-East` (configured with 2 Fault domains and 5 Update domains) in the `East US` region.
2. **Deploy First VM:** Provisioned a Windows Server 2025 virtual machine named `EAST01`, joining it to `AvailSet-East`.
3. **Networking & Security:** Connected `EAST01` to `vNet-East` (`Subnet-East`). Set the Public IP to **None** and created an NSG (`EAST01-nsg`) allowing inbound HTTP (80) and HTTPS (443).
4. **Load Balancer Integration:** Placed the VM securely in the `BE-LBEast` backend pool behind `LB-East`.

![Deploy EAST01 Validation](images/1%20-%20Deploy%20and%20Configure%20EAST01%20validation.png)
![EAST01 Networking](images/1%20-%20Deploy%20and%20Configure%20EAST01%20validation1.png)

---

### Task 2: Provisioning `EastUS02`
1. Provisioned the second regional VM named `EastUS02` in the `East US` region, assigning it to the `AvailSet-East` to ensure hardware-level redundancy.
2. Mirrored the networking configuration (No Public IP) and successfully added it to the `LB-East` backend pool.

---

### Task 3: Dual-Method IIS Installation
Identical to the West region, two different management methods were utilized to install the IIS Web Server role:

**1. GUI Method via Azure Bastion (`EAST01`)**
Successfully established an RDP session to `EAST01` directly from the Azure portal using the Bastion host. Installed the Web Server (IIS) role manually via Server Manager.

**2. Automation Method via Run Command (`EastUS02`)**
To ensure rapid deployment without direct OS access, the Run Command feature was utilized to execute the remote script:
`Install-WindowsFeature Web-Server -IncludeManagementTools`
The script returned a success exit code.

![Run Command Execution](images/2%20-%20Deploy%20and%20Configure%20IIS%20in%20EAST01%20using%20bastion%20add%20role%20IIs%201.png)

---
*✅ Phase 6 Completed Successfully! The Compute Layer is now fully deployed and configured across two global regions.*