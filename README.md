# Active Directory Monitoring with Prometheus and Grafana  

## 📌 Project Overview  
This project implements a monitoring solution for **Active Directory Domain Services (AD DS)** using **Prometheus** and **Grafana**.  

Active Directory is a critical service that manages authentication, authorization, and directory services in enterprise environments. This setup provides **real-time visibility** into AD performance, availability, and security by collecting and visualizing metrics from the AD domain controller.  

---

## 🛠️ Tools & Technologies  
- **Active Directory Domain Services (Windows Server)**  
- **Ubuntu Server** (Prometheus & Grafana host)  
- **Prometheus** – Monitoring and metrics collection  
- **Grafana** – Visualization and dashboards  
- **Windows Exporter** – Exposes AD and Windows Server metrics  
- **Node Exporter** (optional for Linux servers)  

---

## ⚙️ System Architecture  
```text
Windows AD Server (192.168.18.141)
   ↳ Windows Exporter → Prometheus (Ubuntu Server) → Grafana Dashboards


🚀 Installation & Setup
1. Active Directory Server (Windows)

Install and configure Active Directory Domain Services.

Download and install Windows Exporter:
👉 windows_exporter releases

Run the exporter (default port 9182).

2. Prometheus (Ubuntu Server)
# Install Prometheus
sudo apt update
sudo apt install prometheus -y


Edit Prometheus config (/etc/prometheus/prometheus.yml) and add AD target:

scrape_configs:
  - job_name: 'windows_ad'
    static_configs:
      - targets: ['192.168.18.141:9182']


Restart Prometheus:

sudo systemctl restart prometheus

3. Grafana (Ubuntu Server)
# Install Grafana
sudo apt install -y adduser libfontconfig1
wget https://dl.grafana.com/oss/release/grafana_10.0.0_amd64.deb
sudo dpkg -i grafana_10.0.0_amd64.deb

# Start service
sudo systemctl enable grafana-server
sudo systemctl start grafana-server


Access Grafana: http://192.168.18.141:3000

Default login: admin / admin

Add Prometheus as a data source (http://localhost:9090).

Import AD monitoring dashboards.

📊 Dashboards & Metrics
Monitored Metrics:

System Health: CPU, RAM, disk usage

Authentication Services: LDAP response time, Kerberos requests

Replication Status: Domain controller replication health

Security: Logon successes, failures, brute-force attempts

Sample Dashboards:

AD Server Performance Overview

Authentication & Replication Monitoring

Security & Login Failures

🔔 Alerts

Configure Grafana/Prometheus alerts for:

High CPU / Memory usage

Low disk space

LDAP/Kerberos downtime

High number of failed logins

✅ Benefits

Real-time monitoring of AD services

Early detection of performance or security issues

Visual dashboards for admins

Alerts for proactive incident response

📌 Future Enhancements

Integration with Alertmanager for email/Slack alerts

SIEM integration for deeper security analysis

Monitoring of Group Policy and DNS health
