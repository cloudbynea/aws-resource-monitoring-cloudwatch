# AWS Resource Monitoring – CloudWatch Metrics, Alarms, and Automated EC2 Recovery
This project implements proactive monitoring and automated remediation for EC2 instances using Amazon CloudWatch. It simulates a real-world operational scenario where delayed issue detection can cause outages across critical systems.

This solution was developed using AWS Cloud Quest and adapted into a production-style workflow for Technical Account Management, Cloud Support, Cloud Operations, and SRE roles.

---

## 1. Problem Context
A utility company relies on EC2 instances to power essential city infrastructure. When CPU or memory usage spikes, outages may occur before engineers notice system degradation. The organization needs a centralized monitoring system that:

- Detects abnormal resource behavior in real time  
- Sends automated notifications to engineers  
- Triggers self-healing actions to restore service without manual intervention  

---

## 2. Objectives

### Practice Lab Goals
- Investigate default monitoring of Amazon EC2 instances  
- Build a CloudWatch dashboard and add CPU metrics  
- Create a CloudWatch alarm for CPU idle time  
- Configure an SNS notification action  

### DIY Goals
- Add a dashboard widget for memory usage (`mem_used`)  
- Create a memory alarm using a threshold greater than 300M (300,000,000)  
- Attach an EC2 reboot action triggered when memory utilization exceeds the threshold  

---

## 3. Architecture Overview
Server_1, Server_2, Server_3
│
├── Publish Metrics (CPU_IDLE, mem_used)
│
Amazon CloudWatch
├── Dashboard Widgets (CPU, Memory)
├── Alarm: CPU Idle ≤ 20% → SNS Notification
└── Alarm: mem_used ≥ 300M → EC2 Reboot Action

Amazon SNS → Email Notification to Engineer
Amazon EC2 → Automated Instance Reboot (High Memory Utilization) 


---

## 4. Implementation Summary

### 4.1 CloudWatch Metrics
- Metrics retrieved from the custom namespace: `PowerPlantMetrics`
- CPU idle time (`CPU_USAGE_IDLE`) and memory usage (`mem_used`) selected per instance

### 4.2 CloudWatch Dashboard
Dashboard created: **Power-Plant-Dashboard**

Widgets:
- `Servers Idle CPU Usage` (bar graph)
- `Memory Utilization – mem_used` (bar or line graph)

These provide real-time visibility across all three servers.

### 4.3 CPU Alarm
- Metric: `CPU_USAGE_IDLE`
- Threshold: ≤ 20% idle (≈ ≥ 80% CPU usage)
- State trigger: **In Alarm**
- SNS Topic: `High_CPU_USAGE`
- Email notification sent upon state transition

### 4.4 Memory Alarm (with EC2 Automated Recovery)
- Metric: `mem_used`
- Threshold: ≥ 300,000,000  
- Alarm name: `High-Memory-Usage`
- EC2 Action: **Reboot this instance**

This mirrors auto-healing patterns used in production environments.

---

## 5. Validation
Validated requirements:
1. Dashboard widget added for `mem_used`  
2. CloudWatch alarm configured with `mem_used > 300M`  
3. EC2 Reboot Action attached  
4. Correct Instance ID submitted to the Cloud Quest validator  

All validations passed.

---

## 6. Key Learnings
- Visibility is the foundation of operational excellence  
- CPU idle time is a strong indicator of system saturation  
- Memory alarms are effective for detecting leaks or heavy compute workloads  
- SNS + EC2 actions enable fully automated detection + recovery workflows  
- Understanding namespaces, dimensions, and metric grouping is critical  

---

## 7. Technologies Used
- AWS EC2  
- AWS CloudWatch (Metrics, Dashboards, Alarms)  
- Amazon SNS  
- EC2 Recovery Actions  
- AWS Cloud Quest Lab Environment  

---

## 8. Repository Structure

/resource-monitoring/
│── README.md
│── diagrams/
│ └── architecture.png
│── screenshots/
│ ├── dashboard.png
│ ├── cpu-alarm.png
│ ├── memory-alarm.png
│ ├── sns-subscription.png
│ └── ec2-action.png
└── notes/
└── manual-steps.txt

---

## 9. How This Demonstrates Cloud Skills
This project demonstrates:

- Monitoring strategy  
- Incident prevention  
- Automated remediation  
- Operational readiness  
- Customer-impact mitigation  
- Cloud-native observability  

