# 🌐 AWS VPC Peering with Public and Private Subnets

This project demonstrates how to set up VPC peering between two Amazon VPCs, each containing a **public** and **private subnet**, and how to enable secure communication between the two VPCs using **AWS Free Tier** resources.

---

## 🗺️ Architecture

<img src="./architecture.png" width="800" alt="Architecure"/>

---

## 📌 Project Objectives

- Create two VPCs (A & B) with both public and private subnets.
- Establish VPC Peering between the two VPCs.
- Update route tables to allow communication across VPCs.

---

## 🧰 Services Used

- Amazon VPC
- Subnets (Public & Private)
- Route Tables
- VPC Peering
- Internet Gateway (optional)
- EC2 (optional, for testing)

---

## 📐 Network Design

### 🔹 VPC A
- **CIDR**: `10.10.0.0/16`
- **Public Subnet**: `10.10.0.0/20` (e.g. `us-east-1a`)
- **Private Subnet**: `10.10.16.0/20` (e.g. `us-east-1b`)

### 🔹 VPC B
- **CIDR**: `10.20.0.0/16`
- **Public Subnet**: `10.20.0.0/20` (e.g. `us-east-1a`)
- **Private Subnet**: `10.20.16.0/20` (e.g. `us-east-1b`)

💡 Availability Zone (AZ) names like `us-east-1a` are **mapped differently** per account. You can use the same AZ name across VPCs.

---

##  Step-by-Step Setup

### 1️⃣ Create VPCs

Create VPC A and VPC B from the VPC Dashboard:
- Name each VPC
- Assign CIDR blocks as shown above
<img src="./VPCs-CIDRs.png" width="800" />

---

### 2️⃣ Create Subnets

For each VPC:
- Add **two subnets**:
  - 1 Public
  - 1 Private
- Choose appropriate AZs (can be reused between VPCs)
<p float="left">
  <img src="./VPC-A-Subnets.png" width="47%" />
  <img src="./VPC-B-Subnets.png" width="47%" />
</p>
---

### 3️⃣ Create Internet Gateway (optional)

To allow internet access from public subnets:
- Create an **Internet Gateway**
- Attach it to VPC A
- Update VPC A's public subnet route table:
  - `0.0.0.0/0` → Internet Gateway

---

### 4️⃣ Create VPC Peering Connection

1. Go to **VPC > Peering Connections**
2. Click **Create Peering Connection**
3. Set:
   - **Requester VPC**: VPC A
   - **Accepter VPC**: VPC B
4. Accept the peering request
5. Wait until status is `Active`

<img src="./VPC-Connection.png">

---

### 5️⃣ Update Route Tables

Update route tables for all subnets in **both VPCs**:

#### VPC A Routes:
- **Destination**: `10.20.0.0/16` → Target: Peering Connection ID

#### VPC B Routes:
- **Destination**: `10.10.0.0/16` → Target: Peering Connection ID

✅ Add these entries to both **public** and **private** subnets in each VPC.

<img src="./VPC-routes-tables.png" width="800"/>

---

### 6️⃣ (Optional) Launch EC2 Instances

To test cross-VPC connectivity:
- Launch EC2 in VPC A Public Subnet
- Launch EC2 in VPC B Private Subnet
- Allow ICMP or SSH in security groups for testing

---

## 🧹 Clean-Up Instructions

To avoid charges:

1. **Terminate EC2 instances** (if any)
2. **Release Elastic IPs** (if allocated)
3. **Delete VPC Peering Connection**
4. **Delete custom route entries** from all subnets
5. **Delete subnets**
6. **Delete Internet Gateway** (if created)
7. **Delete VPCs**

---

## 🧾 References

- [AWS VPC Peering Documentation](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html)
- [AWS Free Tier Info](https://aws.amazon.com/free)

---

## 🏁 Conclusion

This project covered building two isolated VPCs with structured public and private subnets and securely connecting them using **VPC Peering**. 

---

###### 🤗 My blog’s got diagrams, dev rants, and dopamine

<a href="https://greystack.hashnode.dev" target="_blank">
  <svg width="220" height="30" viewBox="0 0 260 32" xmlns="http://www.w3.org/2000/svg">
    <defs>
      <!-- Gradient for badge background -->
      <linearGradient id="badgeGrad" x1="0%" y1="0%" x2="100%" y2="100%">
        <stop offset="0%" stop-color="#08627eff" />
        <stop offset="100%" stop-color="#3d056bff" />
      </linearGradient>
      <!-- Path for animated border -->
      <path id="borderPath" d="M8,0 H252 A8,8 0 0 1 260,8 V24 A8,8 0 0 1 252,32 H8 A8,8 0 0 1 0,24 V8 A8,8 0 0 1 8,0 Z" />
      <!-- Gradient for border stroke -->
      <linearGradient id="glowGrad" x1="0%" y1="0%" x2="100%" y2="0%">
        <stop offset="0%" stop-color="#b8f0ffff" />
        <stop offset="100%" stop-color="#6aff45ff" />
      </linearGradient>
    </defs>
    <!-- Gradient background -->
    <rect width="260" height="32" rx="8" fill="url(#badgeGrad)" />
    <!-- Text label -->
    <text x="130" y="21" text-anchor="middle" fill="#ffffff" font-family="Verdana" font-size="14">
      ☁️ Greystack Cloud & Code ⚡
    </text>
    <!-- Animated border stroke -->
    <path d="M8,0 H252 A8,8 0 0 1 260,8 V24 A8,8 0 0 1 252,32 H8 A8,8 0 0 1 0,24 V8 A8,8 0 0 1 8,0 Z"
          fill="none" stroke="url(#glowGrad)" stroke-width="3"
          stroke-dasharray="1000" stroke-dashoffset="0">
      <animate attributeName="stroke-dashoffset" values="1000;0" dur="3s" repeatCount="indefinite" />
    </path>
  </svg>
</a>


###### 📲 Feel free to connect or drop feedback on [Aubrey T Dube LinkedIn](https://www.linkedin.com/in/aubrey-t-dube-194896288/) or [GitHub](https://github.com/greytyler)
