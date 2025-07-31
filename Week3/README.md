## 🖥️ Launch a Windows Server EC2 Instance

This project demonstrates how to launch a **Microsoft Windows Server 2019** instance on AWS EC2, securely access it using **Remote Desktop Protocol (RDP)**, and ensure proper security and cost control measures are followed — all within the **AWS Free Tier**.

---

#### 🌐 Architecture 
<img src="./architecture.png" width="800" alt="architecture" />


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

<img src="./W3-Solution-a.png" width="800">
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

###### Connection to windows:
<img src="./W3-Solution-b.png" width="800">


---

#### ✅ Conclusion

This task showed how to provision and remotely access a Windows server in the cloud using AWS EC2. You configured proper security via security groups, and used key-based authentication.

By completing this, you've gained real-world experience with:
- Windows Server provisioning
- Remote access setup
- Key management and password decryption

---

🔐 **Cloud Skills Unlocked** | 🧠 **RDP Security Understood** | 🌍 **First Step Toward Real Infrastructure Deployment**


---

#### 🧹 Cleanup:

- ###### Stop (to reuse later): EC2 Console → Select instance → Instance State → Stop
- ###### Terminate (delete forever): EC2 Console → Select instance → Instance State → Terminate

