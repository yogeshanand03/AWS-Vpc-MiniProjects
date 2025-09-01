# AWS VPC Project

This project demonstrates how to create and configure a **Virtual Private Cloud (VPC)** in AWS with both **Public** and **Private** subnets. The setup ensures that the Public EC2 instance has direct internet access, while the Private EC2 instance accesses the internet through a NAT Gateway.

---

## Steps to Create and Configure the VPC

### 1. Create VPC
- Create a custom VPC with a CIDR block (e.g., `10.0.0.0/16`).

### 2. Create Subnets
- Create **Public Subnet** and **Private Subnet** in different Availability Zones.
- Assign appropriate CIDR blocks (e.g., `10.0.1.0/24` for Public, `10.0.2.0/24` for Private).

### 3. Create Internet Gateway (IGW)
- Create an Internet Gateway and attach it to the VPC.

### 4. Create Route Tables
- Create two Route Tables:
  - **Public Route Table** → Associate with the Public Subnet.
  - **Private Route Table** → Associate with the Private Subnet.

### 5. Configure Public Route Table
- Edit routes in the Public Route Table.
- Add a route to `0.0.0.0/0` pointing to the **Internet Gateway (IGW)**.
- Do not add IGW to the Private Route Table.

### 6. Create Security Groups
- **Public SG** → Allow inbound RDP, HTTP/HTTPS, SSH from `0.0.0.0/0`.
- **Private SG** → Restrict access, allow only traffic from the Public SG.

### 7. Launch EC2 Instances
- Create **one EC2 in the Public Subnet** (with Public SG).
- Create **one EC2 in the Private Subnet** (with Private SG).

### 8. Test Public EC2
- Connect to the Public EC2 via RDP/SSH and verify internet access.

### 9. Create NAT Gateway
- Create a **NAT Gateway** in the Public Subnet.
- Allocate an Elastic IP and associate it with the NAT Gateway.
- Update the **Private Route Table** → Add a route `0.0.0.0/0` pointing to the NAT Gateway.

### 10. Test Private EC2
- Connect to the Private EC2 **via the Public EC2 (bastion host)**.
- Verify connectivity and confirm internet access via NAT Gateway.

---

## Architecture Diagram (High-Level)





VPC
├── Public Subnet (10.0.1.0/24)
│ ├── EC2 (Public)
│ └── Internet Gateway
│
├── Private Subnet (10.0.2.0/24)
│ ├── EC2 (Private)
│ └── NAT Gateway (via Public Subnet)
│
└── Route Tables
├── Public RT → IGW
└── Private RT → NAT


---

## Verification
- ✅ Public EC2 can directly access the internet.
- ✅ Private EC2 uses the NAT Gateway for internet connectivity.
- ✅ Security Groups enforce controlled access.

---

## Tools & Services Used
- **AWS VPC**
- **EC2**
- **Internet Gateway**
- **NAT Gateway**
- **Security Groups**
- **Route Tables**

---

## Author
Project created by **Yogesh** as part of AWS VPC learning.






