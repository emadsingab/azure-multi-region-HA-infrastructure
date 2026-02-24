# Enterprise Multi-Region Azure Infrastructure 🌐

🎯 Project Overview

This project demonstrates a highly available, multi-region cloud infrastructure deployed on Microsoft Azure. It mirrors real-world enterprise deployment strategies to ensure business continuity, security, and scalable performance across different geographic locations.

The project aims to showcase:
* Multi-Region High Availability
* Secure Network Topologies (Hub-and-Spoke concept)
* Traffic Load Balancing
* Automated Disaster Recovery capabilities

🖥️ Components

| Component | Description |
| :--- | :--- |
| **Virtual Networks (vNets)** | Logical isolation of the Azure cloud configured with custom IP spaces across two distinct regions (e.g., East US & West US). |
| **vNet Peering** | Secure, low-latency interconnection bridging the regional virtual networks. |
| **NAT Gateways** | Managed outbound internet connectivity for internal virtual machines, preventing direct inbound exposure. |
| **Azure Bastion** | Fully managed PaaS providing secure and seamless RDP/SSH connectivity to VMs directly from the Azure portal. |
| **Azure Load Balancers** | Layer 4 traffic distribution to ensure high availability of compute resources. |
| **Blob Storage** | Object storage configured with asynchronous Object Replication across regions for backup and disaster recovery. |

🛠️ Prerequisites

To replicate this environment, you will need:
* An active Microsoft Azure Subscription
* Azure CLI installed locally (Optional, for scripting)
* Basic understanding of CIDR notation and IP addressing

⚡ Deployment Instructions

1. **Foundational Networking:**
   Deploy a central Resource Group to contain the lab assets. Following that, provision two Virtual Networks (vNets) in separate regions, carving out specific subnets for workloads and Bastion services.
2. **Secure Outbound Access:**
   Deploy two NAT Gateways and attach them to the respective subnets to route outbound traffic securely.
3. **Compute & Availability:**
   Provision Virtual Machines within Availability Sets in both regions. Ensure these VMs do not have Public IPs attached directly to their network interfaces.
4. **Inter-Region Connectivity:**
   Establish vNet Peering between the two regional networks to allow private traffic flow.

⚙️ Implementation Details & Best Practices

✅ 1. Network Security Integration
The architecture strictly avoids assigning Public IPs to workload VMs. All inbound administration is tunneled through Azure Bastion, while outbound internet access (for updates/patches) is routed via NAT Gateways, ensuring a hardened security posture.

✅ 2. Storage Replication
Azure Blob Storage is utilized with Object Replication rules established. This ensures that any data written to the primary region's storage account is automatically and asynchronously copied to the secondary region.

📂 Project Structure

.
├── images/
│   ├── architecture-diagram.png  # Overall topology
│   ├── vnet-peering.png          # Configuration proof
│   └── ...
├── scripts/
│   └── deploy-infrastructure.azcli # Azure CLI deployment commands
└── README.md                     # Project documentation

🔧 Features

* Enterprise-grade logical separation using subnets and vNets.
* Centralized and secure remote administration without opening public SSH/RDP ports.
* Resilient architecture designed to withstand regional outages.
* Adherence to Microsoft Cloud Adoption Framework (CAF) networking best practices.

🎓 Author

**Emad Elsayed Singab**
System Administrator & Cloud Engineer | Certified Microsoft Azure Administrator (AZ-104) | Mansoura University Engineering Alumni
