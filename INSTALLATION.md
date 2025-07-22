## Setup Instructions (Azure VM + T-Pot using PuTTY & Git)

This section describes how the T-Pot honeypot was manually installed on an Azure VM using Git, accessed via **PuTTY** on Windows.

---

### 1. Create Azure VM

- **OS**: Ubuntu 20.04 LTS
- **Size**: Standard\_B1s (Free tier eligible)
- **Inbound Ports Opened**: 22 (SSH) during setup

---

### 2. SSH Access using PuTTY

- Launch PuTTY
- Enter the **Azure VM public IP**
- Use Port `22` and SSH protocol
- (Optional) If using key-based auth, load your `.ppk` file under `Connection > SSH > Auth`

Once connected, log in with your VM credentials.

---

### 3. Install T-Pot from GitHub

Run the following commands in the PuTTY terminal:

```bash
# Step 1: Update and upgrade system
sudo apt update
sudo apt upgrade -y

# Step 2: Install Git
sudo apt install git -y

# Step 3: Clone the official T-Pot repository
sudo git clone https://github.com/telekom-security/tpotce

# Step 4: Change to cloned directory
cd tpotce

# Step 5: Run the installer script
sudo ./install.sh
```

>  During installation, select the honeypot profile (e.g., **Standard** for all services). You’ll also be asked to set a secure password for the web interface.

---

### 4.  Reboot After Installation

```bash
sudo reboot
```

T-Pot services start automatically after reboot.

---

### 5.  Open Honeypot Ports in Azure

Update the **Inbound Rules** in the Azure Network Security Group to allow a wide range of ports for full honeypot interaction.

- **Port Range**: `1-65535`
- **Protocol**: `Any`
- **Source**: `Any` (0.0.0.0/0)

> Note: This configuration exposes the VM to all types of external traffic. Use only in isolated test environments and **never for production workloads**.




### 6. Access Kibana Dashboard

Once all services are up and the correct ports are opened:

 Visit: `http://<your_vm_public_ip>:64297`\
 Login to view the real-time honeypot dashboards.



