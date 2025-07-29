# 🏡 Real Estate Finder – Network Architecture Design
![15c6ac4a-152f-4eca-b9e8-1ee14d264343](https://github.com/user-attachments/assets/63e91e75-b707-4a1c-86b4-70812fb316e9)

![Architecture Diagram](diagram.png)  
*Figure: Network Architecture for Real Estate Finder Platform*

---

## 📝 Assumptions

- The platform is deployed on AWS with multi-region and multi-AZ support.
- Each Availability Zone contains both public and private subnets.
- EC2 instances are used for hosting frontend/backend services.
- Amazon RDS is used for managing structured data (listings, user info, transactions).
- A NAT Gateway is configured to allow private subnets to access the internet securely.
- Users from different countries can access the system with low latency via Route 53.
- 3rd-party APIs are accessed via secure endpoints.
- Developers use a separate VPN or Bastion host for remote access.
- Application is containerized and could be migrated to ECS/EKS later if needed.

---

## 📘 Summary

### 🔧 Project Details
This project outlines a scalable and secure cloud network architecture for a real estate finder platform. The system allows users to search, bid, and communicate regarding property listings. It integrates with multiple 3rd-party services to fetch updated listings and supports both development and production environments.

### 📐 Architecture Decisions
- Chose AWS for cloud infrastructure due to its global availability and services.
- Used two regions (e.g., Asia-Pacific and North America) for geographical fault tolerance.
- Each region has two Availability Zones to ensure high availability.
- Public subnets house NAT Gateways and Load Balancers.
- Private subnets host EC2 instances for applications and Amazon RDS for data storage.

### 🧠 Reasoning
- NAT Gateways prevent direct internet access from the database layer, improving security.
- Multi-region deployment ensures data locality and fast access.
- Load balancing and Auto Scaling ensure the system handles different levels of user traffic.
- Centralized logging and monitoring are assumed through CloudWatch (not shown in diagram).

### 🧩 Networking Components
| Component          | Use Case                                      |
|--------------------|-----------------------------------------------|
| VPC                | Isolated network environment                  |
| Subnets (Public/Private) | Separation of roles (web vs data layer) |
| NAT Gateway        | Secure outbound internet for private subnet   |
| EC2 Instances      | Host applications (frontend/backend)          |
| RDS (Database)     | Store property listings and user data         |
| Internet Gateway   | Enables internet access to public subnet      |
| Route 53           | DNS-based routing across regions              |

---

## 💰 Cost Estimates

| Users                | Compute Cost (EC2) | Database Cost (RDS) | Bandwidth | Total (USD/month) |
|----------------------|-------------------|----------------------|-----------|--------------------|
| 100 Concurrent       | $30               | $15                  | $10       | ~$55               |
| 10,000 Concurrent    | $400              | $200                 | $150      | ~$750              |
| 100,000 Concurrent   | $1,500            | $1,000               | $700      | ~$3,200            |
| 1 Lakh Monthly       | $100              | $50                  | $20       | ~$170              |
| 10 Lakh Monthly      | $600              | $300                 | $250      | ~$1,150            |
| 100 Million Monthly  | $4,000            | $2,000               | $2,000    | ~$8,000            |

> ⚠️ *These are rough estimates and may vary based on AWS pricing tiers, data egress, and specific configurations.*

---

## ✅ Submission Info
- Author: *Your Name*
- Platform: AWS (assumed)
- Tool Used for Diagram: Excalidraw (or your selected tool)
- Deadline: 19-07-2025
