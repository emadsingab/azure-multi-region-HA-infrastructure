# 3. Deploy Azure Bastion & VNet Peering 🛡️

## 🎯 Section Goal
Establish private connectivity between `vNet-West` and `vNet-East` via virtual network peering, and deploy a centralized, secure remote access solution with Azure Bastion.

---

## 🚀 Task 1: Configure VNet Peering

**Theoretical Concept:**
VNet Peering enables seamless, private connectivity between two virtual networks. Traffic between peered virtual networks is kept entirely on the Microsoft backbone network, providing a highly secure and reliable connection without needing public internet, gateways, or encryption. This allows resources in `vNet-West` and `vNet-East` to communicate securely as if they were part of the same local network.

**Implementation Steps:**

1. **Navigate to Peerings:** Accessed `vNet-West` from the Azure Portal, navigated to the **Settings** section, and selected **Peerings**. Clicked **+ Add** to initiate the connection.
   ![Navigate to Peerings](images/1%20-%20Configure%20vNet%20Peering.png)

2. **Configure Reciprocal Peering:**
   - Set up the primary peering link from `vNet-West` to `vNet-East`.
   - Simultaneously configured the reciprocal link from `vNet-East` back to `vNet-West` (named `vNetEast-vNetWest`) within the same wizard.
   - Permitted forwarded traffic and virtual network access across both ends to ensure full bi-directional communication.
   ![Configure Peering](images/1%20-%20Configure%20vNet%20Peering3.png)

3. **Verify Connectivity:** Validated that the peering status updated to **Connected** on both virtual networks, confirming successful inter-region private routing.
   ![Peering Connected](images/1%20-%20Peering%20Connected.png)

---

## 🚀 Task 2: Deploy Azure Bastion

**Theoretical Concept:**
Azure Bastion is a fully managed Platform-as-a-Service (PaaS) that provides secure and seamless RDP and SSH connectivity to virtual machines directly from the Azure portal over TLS. It acts as a jump server, eliminating the need to expose VMs to the public internet via Public IP addresses, thereby significantly reducing the external attack surface.

**Implementation Steps:**

1. **Initiate Bastion Deployment:** Navigated to the **Bastion** blade within the `vNet-West` configuration.
2. **Configure Bastion:**
   - Defined the Bastion host name (e.g., `vNet-West-bastion`) and ensured it resides within the centralized `RG-lab` resource group.
   - Configured the required `AzureBastionSubnet` and assigned a dedicated Public IP address specifically for the Bastion service.
   - Clicked **Deploy Bastion** to provision the managed service.
   ![Deploy Bastion](images/2%20-%20Deploy%20Azure%20Bastion.png)

3. **Verify Deployment:** Monitored the deployment process until the provisioning state successfully completed, readying the environment for secure remote VM administration.
   ![Bastion Succeeded](images/2%20-%20Bastion%20Succeeded.png)

---
*✅ Phase 3 Completed Successfully!*