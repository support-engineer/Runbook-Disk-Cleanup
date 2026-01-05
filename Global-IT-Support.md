# Global IT Support Engineering Portfolio

## About Me
I’m a support engineer with experience in **global, follow-the-sun operations**. I specialize in reducing incident noise, automating repetitive tasks, and addressing root causes to prevent recurring issues. My focus is on building **scalable processes, runbooks, and automation** that make support faster, more predictable, and less manual—helping engineers focus on solving problems while users get reliable resolutions anytime, anywhere.

---

## Project 1: Global Incident Response Runbook

**Objective:** Standardize critical incident responses across regions and shifts.

**Key Features:**
- Step-by-step guidance: **Detection → Triage → Escalation → Resolution → Closure**
- Integrated **SLA thresholds** and escalation triggers
- **Known Error Database (KEDB)** integration for documenting recurring issues
- Post-incident review templates to capture lessons learned

**Impact:**
- Reduced MTTR across follow-the-sun shifts
- Enabled seamless handoffs and consistent incident handling
- Allowed Tier 1 engineers to resolve more incidents using **shift-left practices**

---

## Project 2: Automated Server Health Check Script

**Objective:** Automate monitoring and alerting to prevent incident escalation.

**Key Features:**
- Monitors CPU, memory, disk usage, and service health on critical servers
- Sends automated alerts via **email, Teams, or Slack** when thresholds are exceeded
- Optional automated remediation (e.g., service restart)
- Logs results centrally for trend analysis and RCA

**Impact:**
- Reduced repetitive manual work for engineers
- Prevented potential outages by providing early alerts
- Supported **follow-the-sun monitoring** with automated notifications

**Example Snippet:**
```python
import psutil, smtplib
from email.message import EmailMessage

def check_server():
    cpu = psutil.cpu_percent()
    mem = psutil.virtual_memory().percent
    if cpu > 85 or mem > 90:
        send_alert(cpu, mem)

def send_alert(cpu, mem):
    msg = EmailMessage()
    msg.set_content(f"Alert! CPU: {cpu}%, Memory: {mem}%")
    msg['Subject'] = 'Server Health Alert'
    msg['From'] = 'monitoring@company.com'
    msg['To'] = 'oncall@company.com'
    
    with smtplib.SMTP('smtp.company.com') as server:
        server.send_message(msg)

check_server()
