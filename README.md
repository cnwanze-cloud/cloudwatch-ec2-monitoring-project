# CloudWatch EC2 Monitoring Project

## Overview

This project demonstrates how to build a production-style monitoring and logging system on AWS using Amazon CloudWatch.

It focuses on observability, ensuring that infrastructure and applications are:

- Measurable (metrics)  
- Traceable (logs)  
- Alertable (alarms)  

> The goal is simple: detect issues before users notice them.

---

## Objectives

- Monitor EC2 instance performance (CPU, network, status)
- Collect and centralize application/system logs
- Trigger alerts based on abnormal conditions
- Visualize system health using dashboards
- Simulate failures to validate monitoring reliability

---

## Architecture
<img width="1408" height="768" alt="Architectural Diagram" src="https://github.com/user-attachments/assets/159aeea4-99bf-4d15-872e-6fa4e0fb7a09" />



---

## Services Used

* Amazon EC2
* Amazon CloudWatch
* Amazon SNS

---

## Project Implementation

### EC2 Setup

* Launched an instance using Amazon Linux 2023
* Configured security group:

  * SSH (22)
  * HTTP (80)
<img width="974" height="475" alt="image" src="https://github.com/user-attachments/assets/62dd89ef-2ab4-487c-996f-b2a3064a115e" />

<img width="966" height="266" alt="image" src="https://github.com/user-attachments/assets/c42e56df-3547-4307-bb7b-5569957a9e20" />


---


### Alarm Configuration

Created a CPU utilization alarm:

* Threshold: `> 70%`
* Period: `5 minutes`
* Action: Send notification via SNS
<img width="974" height="312" alt="image" src="https://github.com/user-attachments/assets/b938622c-ab6f-4611-a1be-3317b82b5693" />

<img width="975" height="380" alt="image" src="https://github.com/user-attachments/assets/b2be2fc3-4343-410b-95db-5fad146617f6" />


---

### Notifications (SNS)

* Created SNS topic
* Subscribed email endpoint
* Confirmed subscription

✔ Enables real-time alerting when thresholds are exceeded
<img width="895" height="395" alt="image" src="https://github.com/user-attachments/assets/476ad7dc-1029-4bd2-979e-f45613595512" />


---

### Failure Simulation (CPU Stress Test)

```bash
yes > /dev/null &
```
<img width="975" height="137" alt="image" src="https://github.com/user-attachments/assets/3673285c-3c4a-4e87-8529-2f836af4ff9e" />

**Result:**

* CPU spikes
* Alarm transitions: `OK → ALARM`
* Email notification triggered
<img width="975" height="335" alt="image" src="https://github.com/user-attachments/assets/3d575907-d7bd-4fd2-ab26-e357fd28603b" />

<img width="975" height="167" alt="image" src="https://github.com/user-attachments/assets/a7d121c2-b668-4390-9b3e-d5abb96c208c" />

<img width="975" height="517" alt="image" src="https://github.com/user-attachments/assets/e4c6d313-40c5-47ed-8e20-38b0ed33a827" />


---

### Log Collection with CloudWatch Agent

#### Installation

```bash
sudo yum install -y amazon-cloudwatch-agent
```
<img width="844" height="170" alt="image" src="https://github.com/user-attachments/assets/38b1ec3b-362d-43a3-9b26-5955ba7deafb" />

---

#### IAM Role Setup

Attached policy:

* `CloudWatchAgentServerPolicy`
<img width="973" height="187" alt="image" src="https://github.com/user-attachments/assets/6a167e66-585a-43b8-a06e-bbef3f47a660" />

---

#### Configuration

Monitored log file:

```text
/var/log/cloudwatch-demo.log
```

---

#### Start Agent

```bash
sudo systemctl start amazon-cloudwatch-agent
```

---

### Centralized Logging

Logs are sent to:

* CloudWatch Logs → Log Groups → `cloudwatch-demo`

✔ Enables:

* Log aggregation
* Real-time monitoring
* Debugging
<img width="975" height="193" alt="image" src="https://github.com/user-attachments/assets/4c27abd8-80b6-4ecf-bd55-2678b23d81ff" />


---

### Dashboard Creation

Built a custom dashboard in Amazon CloudWatch

**Widgets included:**

* CPU Utilization graph
* Network in/out

✔ Provides real-time system health visibility

<img width="975" height="389" alt="image" src="https://github.com/user-attachments/assets/0ba29b85-b01e-49b6-a16a-d7dcc6eb8ac1" />

---

## Testing & Validation

| Test Case           | Expected Result         | Status |
| ------------------- | ----------------------- | ------ |
| CPU stress          | Alarm triggers          | ✅      |     |
| Alarm notification  | Email received          | ✅      |
| Dashboard update    | Real-time visualization | ✅      |


---

## Skills Demonstrated

* AWS Infrastructure Setup
* Monitoring & Observability
* Incident Detection & Alerting
* Troubleshooting & Debugging

---

## Conclusion

This project goes beyond deployment by focusing on visibility, reliability, and proactive incident detection

It demonstrates how modern cloud systems are monitored in real-world production environments using Amazon CloudWatch.

