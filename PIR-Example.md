## Post-Incident Review (PIR): Incident #IM-2026-042

**Date:** January 2, 2026

**Incident Manager:** William Parker

**Severity:** P1 (Critical) - Potential Total Site Outage

### 1. Executive Summary

During a high-traffic marketing campaign, the primary IIS Web Server experienced a rapid surge in log generation. Without intervention, the disk would have reached 100% capacity, causing a total service crash. **Runbook RB-2026-004** triggered automatically, remediating the issue in under 30 seconds with zero user impact.

### 2. Incident Timeline (The "Detect-to-Recover" Flow)

| Time (UTC) | Event | Action Taken |
| --- | --- | --- |
| **14:00:00** | **Alert Triggered** | Monitoring detected C: Drive at 91% capacity. |
| **14:00:05** | **Auto-Trigger** | Orchestration engine initiated `RB-2026-004-DiskCleanup.ps1`. |
| **14:00:12** | **Remediation** | Script purged 14GB of legacy logs and temp files. |
| **14:00:25** | **Verification** | Script confirmed disk usage dropped to 74%. |
| **14:00:30** | **Notification** | Success alert sent to Microsoft Teams; Incident auto-closed. |

---

### 3. Root Cause Analysis (The 5 Whys)

1. **Problem:** The server was at risk of a crash.
2. **Why?** The C: drive was almost full.
3. **Why?** IIS logs were accumulating faster than usual due to high traffic.
4. **Why?** The default log rotation policy was too infrequent for peak periods.
5. **Why? (Root Cause):** Lack of dynamic log management—**resolved via Hyperautomation.**

### 4. ROI & Value Realization

* **Manual MTTR (Estimated):** 45 Minutes (Time to page engineer + login + manual delete).
* **Automated MTTR (Actual):** 30 Seconds.
* **Toil Saved:** 100% (No human intervention required).
* **Business Impact:** Prevented an estimated $15,000 in lost revenue from potential downtime.
