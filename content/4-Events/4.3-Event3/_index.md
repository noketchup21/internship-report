---
title : "Event 3"
date : "2025-09-09"
weight : 3
chapter : false
pre : " <b> 4.3 </b> "
---


# Summary Report: “AWS Well-Architected Security Pillar”

## Event Objectives
* Master the five domains of the Security Pillar within the AWS Well-Architected Framework.
* Understand core security principles: Zero Trust, Least Privilege, and Defense in Depth.
* Learn to architect secure identity management (IAM) and infrastructure protection.
* Implement continuous detection and automated incident response strategies.
* Explore data protection techniques using KMS and encryption best practices.

## Speakers
* **AWS Security Solutions Architects**
* **Cloud Security Specialists**

## Key Highlights

### Security Foundation & Identity (IAM)
* **Core Principles:** Adopting a "Zero Trust" mindset and "Defense in Depth" (layering security controls).
* **Threat Landscape:** Analysis of top cloud security threats specific to the Vietnamese market.
* **Modern IAM:** Moving away from long-term credentials (access keys) to temporary credentials using IAM Roles.
* **Access Control:** Implementing **IAM Identity Center** for SSO and using Service Control Policies (SCPs) to set permission boundaries in multi-account environments.
* **Validation:** Using **IAM Access Analyzer** to verify policies and permissions.

### Detection & Infrastructure Protection
* **Continuous Monitoring:** Centralizing visibility with **CloudTrail** (org-level), **GuardDuty** (threat detection), and **Security Hub**.
* **Logging Strategy:** Enabling logs at every layer—VPC Flow Logs for network traffic and ALB/S3 logs for access patterns.
* **Network Security:** Implementing VPC segmentation (public vs. private subnets) and layering **Security Groups** (stateful) with **NACLs** (stateless).
* **Edge Protection:** Using **AWS WAF** and **AWS Shield** to protect against DDoS and web exploits.

### Data Protection & Incident Response
* **Encryption:** Managing keys with **AWS KMS** (key rotation, policies) and ensuring encryption at-rest (EBS, RDS, S3) and in-transit.
* **Secrets Management:** replacing hardcoded credentials with **AWS Secrets Manager** and Parameter Store.
* **IR Playbooks:** Defining standard procedures for scenarios like compromised IAM keys, accidental S3 public exposure, and EC2 malware events.
* **Automation:** Using Lambda and Step Functions to auto-remediate threats (e.g., isolating a compromised instance).

## Key Takeaways

### Security Mindset
* **Shift Left:** Security must be integrated early in the design phase, not added as an afterthought.
* **Identity is the New Perimeter:** In a cloud-native world, strong identity management (IAM) is more critical than traditional network firewalls.
* **Assume Breach:** Design systems assuming an attacker is already inside; focus on limiting the blast radius.

### Technical Architecture
* **Least Privilege:** Grant users and services only the permissions they need to perform their tasks, and nothing more.
* **Detection-as-Code:** Define security rules and alerts using code to ensure consistency and version control.
* **Automated Rotation:** Automate the rotation of database credentials and API keys to minimize the impact of leaked credentials.

### Applying to Work
* **Audit IAM:** Review current project IAM roles to remove unused permissions and enforce MFA for all users.
* **Secure Secrets:** Migrate database credentials from `application.properties` files to **AWS Secrets Manager** in Spring Boot applications.
* **Enable GuardDuty:** Turn on GuardDuty in all accounts to immediately start detecting anomalous behavior.
* **Draft IR Plan:** Create a basic Incident Response playbook for the most likely scenarios (e.g., application exploits).

## Event Experience

The **“AWS Well-Architected Security Pillar”** session provided a deep dive into securing cloud workloads, balancing theoretical frameworks with practical implementation in the Vietnamese context.

### Learning from experts
* Gained insight into the **Shared Responsibility Model**, clarifying exactly which security aspects AWS handles vs. what the customer must secure.
* Learned about common pitfalls in Vietnam, such as inadvertent public data exposure, and how to prevent them.

### Hands-on technical exposure
* **IAM Policy Simulation:** The mini-demo on validating policies showed how to simulate access requests to ensure permissions are configured correctly before deployment.
* **IR Lifecycle:** Walking through the "Compromised IAM Key" playbook highlighted the importance of speed and automation in responding to incidents.

### Networking and discussions
* Discussed the challenges of implementing **Zero Trust** in legacy application architectures.
* Exchanged tips on preparing for the **AWS Certified Security – Specialty** exam.

### Lessons learned
* **Log Everything:** You cannot detect what you do not log. VPC Flow Logs and CloudTrail are essential for forensics.
* **Avoid Long-Term Keys:** Static IAM access keys are a major risk; switching to IAM Roles for EC2/Lambda is a priority.
* **Automation is Security:** Manual security checks scale poorly; automation using EventBridge and Lambda allows for real-time remediation.

### Event photo
![Photo](/images/aws3.jpg)
![Photo](/images/aws32.jpg)
![Photo](/images/aws33.jpg)