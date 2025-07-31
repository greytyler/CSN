## 🖥️ Launch a Windows Server EC2 Instance

This project demonstrates how to launch a **Microsoft Windows Server 2019** instance on AWS EC2, securely access it using **Remote Desktop Protocol (RDP)**, and ensure proper security and cost control measures are followed — all within the **AWS Free Tier**.

---

## 🌐 Architecture Diagram



---

## 🚀 Guide

### ✅ 1. Launch EC2 Instance

- Go to AWS [EC2 Dashboard](https://console.aws.amazon.com/ec2)
- Click **“Launch Instance”**
- Configuration:
  - **Name**: `CSN-Bootcamp-Week3`
  - **AMI**: `Microsoft Windows Server 2019 Base`
  - **Instance Type**: `t2.micro` (Free Tier eligible)
  - **Key Pair**: Create new or use existing `.pem` key (must be downloaded and stored securely)

---

### 🌐 2. Network Settings

- **VPC**: Default (or custom public VPC)
- **Subnet**: Public subnet
- **Auto-assign Public IP**: `Enabled`

---

### 🔐 3. Security Group Configuration

Create a new security group with the following inbound rule:

| Type | Protocol | Port | Source |
|------|----------|------|--------|
| RDP  | TCP      | 3389 | My IP  |

This restricts RDP access to your current IP address, ensuring secure remote login.

---

### 🔓 4. Get Windows Administrator Password

1. Go to **EC2 > Instances**
2. Select your instance → Click **Connect**
3. Under **RDP Client**, click **Get Password**
4. Upload your `.pem` key
5. Click **Decrypt Password**
6. Copy the:
   - **Username**: `Administrator`
   - **Password**: (decrypted string)

---

### 🖥️ 5. Connect via RDP

#### 🪟 Windows:
- Open **Remote Desktop Connection** (`mstsc`)
- Paste public IP address from EC2
- Use `Administrator` and decrypted password

#### 🍎 macOS:
- Install **Microsoft Remote Desktop**
- Add new PC → Use public IP and credentials

---

## 📸 Screenshots to Capture

| Screenshot | Description |
|------------|-------------|
| ✅ EC2 Dashboard | Showing instance named `CSN-Bootcamp-Week3` in **Running** state |
| ✅ Security Group Rules | Inbound RDP (port 3389) open only to **your IP** |
| ✅ Decrypted Password Screen | Showing `Administrator` and the password |
| ✅ RDP Connection | Desktop of the Windows Server instance |

---

#### 🧹 Cleanup:

When you're done, **stop or terminate** the instance:

### Stop (to reuse later):
