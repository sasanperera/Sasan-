# Course 2: Play It Safe - Manage Security Risks

Welcome to my course notes and practical case studies for Course 2 of the Google Cybersecurity Professional Certificate.

---

## 📌 Module 1: Core Security Frameworks & Concepts
* **NIST Cybersecurity Framework (CSF):** Identify, Protect, Detect, Respond, Recover.
* **CIA Triad Focus:** Protecting Confidentiality, Integrity, and Availability across enterprise environments.
* **Security Controls:** Implementing administrative, technical, and physical safeguards.

---

## 📌 Module 2: Incident Analysis Case Study

### Scenario Overview
An online e-commerce storefront experienced repeated web server crashes, causing system downtime and preventing customers from completing transactions. 

### Investigation & Log Examination
To identify the root cause of the crashes and restore availability, key log sources were evaluated:
* **Web Server Error Logs:** Analyzed to check for application-level execution errors, memory leaks, or database connection timeouts.
* **Network & Firewall Logs:** Examined to detect potential volumetric traffic spikes, brute-force attempts, or Distributed Denial of Service (DDoS) attacks.
* **System Resource Logs:** Monitored to evaluate hardware capacity, CPU utilization, and memory usage during the crash window.

### SIEM Utilization & Operational Value
* **Log Aggregation:** Centralized multi-system logs into a single console, eliminating the delay of manually checking disparate system logs.
* **Automated Alerting:** Enabled immediate notification of abnormal traffic spikes and automated threat identification.
* **Visualization:** Dashboard metrics provided clear graphical representations of system metrics to communicate incident impact during audits and management reviews.

---

## 📌 Module 4: Incident Response & Security Playbooks

### What are Incident Response Playbooks?
A **playbook** is a clear, step-by-step document and guide designed to assist security analysts in responding to, mitigating, and resolving specific security risks and threats efficiently and consistently.

### The 6 Lifecycle Stages of a Playbook
1. **Preparation:** Establishing incident response capabilities, tools, policies, and training before an incident occurs.
2. **Identification:** Detecting, analyzing, and determining the scope and severity of a security event.
3. **Containment:** Taking immediate tactical actions to limit the impact and prevent the threat from spreading across the network.
4. **Eradication:** Neutralizing the root cause of the incident by removing malware, revoking compromised credentials, or closing vulnerabilities.
5. **Recovery:** Restoring affected systems, services, and operations safely back to normal production status.
6. **Post-Incident Activity:** Analyzing lessons learned, evaluating response performance, and updating documentation and controls to prevent recurrence.
