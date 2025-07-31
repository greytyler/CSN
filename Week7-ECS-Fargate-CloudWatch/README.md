### 🧱 ECS Fargate + CloudWatch Monitoring

Deploy a containerized app **(NGINX or Grafana)** on **Amazon ECS** using **Fargate**, and monitor CPU/Memory utilization using a **CloudWatch** Dashboard.

<br>

##### Architecture
```
[User's Browser]
       |
       v
[Public Internet]
       |
       v
[AWS VPC]
 ├── [Public Subnet]
 │     ├── [Fargate Task: NGINX/Grafana]
 │     │       └─ CPU + Memory Allocation
 │     └── [Security Group: HTTP (80) / Custom Port]
 |
 └── [CloudWatch Dashboard]
         ├── CPUUtilization Widget
         └── MemoryUtilization Widget
