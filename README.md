# Project: Self-Healing Disk Remediation via Hyperautomation

> **Category:** Site Reliability Engineering (SRE) / IT Service Management (ITSM)  
> **Stack:** PowerShell, JSON, YAML (for CI/CD), REST API

## Overview

This project implements a **Shift-Left** methodology by automating the resolution of "Low Disk Space" incidents on IIS Web Servers. It moves the resolution from a manual Level 2/3 task to a **Level 0 (Self-Healing)** automated workflow.

## The Problem (Toil)

Engineers were manually investigating disk space alerts, clearing temp files, and rotating logs. This resulted in:

* **MTTR:** 45+ minutes (subject to engineer availability).
* **Toil:** High frequency, low-value manual intervention.

## The Solution (Hyperautomation)

An event-driven runbook that integrates with monitoring tools (e.g., Azure Monitor, Zabbix, or Datadog) to trigger a cleanup script immediately upon threshold breach.

### Key Features:

* **Threshold Validation:** Prevents "flapping" by re-verifying disk metrics before action.
* **Intelligent Purge:** Cleans `C:\Windows\Temp` and rotates IIS logs older than 14 days.
* **Verification Loop:** Re-checks metrics post-cleanup.
* **Escalation Logic:** If the cleanup fails to recover space, it triggers a **Major Incident Management (MIM)** alert via Webhook.

## Code

The primary remediation logic is contained in `RB-2026-004-DiskCleanup.ps1`.
