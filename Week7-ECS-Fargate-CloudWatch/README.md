> ### 🧱 ECS Fargate + CloudWatch Monitoring

######  Deploy a containerized app **(NGINX or Grafana)** on **Amazon ECS** using **Fargate**, and monitor CPU/Memory utilization using a **CloudWatch** Dashboard.

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
```

##### 📍 Steps Taken

##### 1. ECS Cluster Created
- Cluster Name: week7-cluster
- Launch type: Fargate


##### 2. Task Definition
- Task Name: week7-task
- CPU: 256 (.25 vCPU)
- Memory: 512 MiB
- Container: nginx or grafana/grafana
- Port: 80 or 3000

<img src="./task-def-cpu-memory-settings.png" width="515"/>

##### 3. ECS Service Deployment
- Service Name: week7-service
- Subnet: Public
- Auto-assign Public IP: Enabled
- Security Group: Allows port 80 or 3000

<img src="./ecs-cluster-service.png" width="515"/>

##### 4. CloudWatch Dashboard
- Dashboard: week7-metrics
- Widgets Added:
- CPUUtilization
- MemoryUtilization

<img src="./cloudwatch-dash-initial.png" width="515"/>

##### 5. Simulated Load
- Action: Auto-refresh browser on public IP to create metric activity
<img src="./cloudwatch-dash-after.png" width="515"/>

## 🧼 Clean-Up Instructions

To stay within the Free Tier:

- ✅ 1. Delete the ECS Service
- ✅ 2. Delete the Running Task (if any)
- ✅ 3. Delete the ECS Cluster distribution
- ✅ 4. Deregister the Task Definition
- ✅ 5. Delete the CloudWatch Dashboard

---

## 📝 License

MIT License — feel free to use the template.


