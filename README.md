# Enterprise Security & Threat Hunting Lab

A multi-phase enterprise security lab featuring an isolated Windows 11 target and an Active Directory Domain Controller for threat hunting, telemetry generation, and policy deployment.

---

## 🧪 Phase 1: Windows 11 Sandbox Provisioning
**Status:** In Progress 🟡

### 🎯 Phase 1 Objectives
- [x] Standardize the Windows 11 ISO naming convention.
- [x] Provision a new VirtualBox Virtual Machine (VM) tailored for Windows 11 minimum requirements.
- [x] Configure an isolated "Sandbox" internal network to prevent accidental network leaks.
- [ ] Install Windows 11 using the offline local account bypass (OOBE\BYPASSNRO).
- [ ] Establish a clean "Baseline" snapshot before introducing any tools or threats.

*📸 Screenshot Placeholders:*
> `[Insert Screenshot: VirtualBox Network Settings showing 'ET-Sandbox' Internal Network]`
> `[Insert Screenshot: Windows 11 Desktop post-installation (Local Account)]`

---

## 🏢 Phase 2: Active Directory Integration
**Status:** Pending 🔴

### 🎯 Phase 2 Objectives
- [ ] Power on `ET-DC01` (Windows Server) and connect it to the `ET-Sandbox` internal network.
- [ ] Configure static IP addressing for both `ET-DC01` and `ET-Win11-Target`.
- [ ] Join `ET-Win11-Target` to the local Active Directory domain.
- [ ] Create test Organizational Units (OUs) and Domain User accounts.
- [ ] Deploy a Group Policy Object (GPO) to the Windows 11 target (e.g., setting baseline security policies or disabling Defender for testing).

*📸 Screenshot Placeholders:*
> `[Insert Screenshot: Windows 11 System Properties showing successful Domain Join]`
> `[Insert Screenshot: Active Directory Users and Computers (ADUC) showing the new ET-Win11-Target machine]`

---

## 🛡️ Phase 3: Telemetry & Log Forwarding
**Status:** Pending 🔴

### 🎯 Phase 3 Objectives
- [ ] Install Sysmon on `ET-Win11-Target` using an enterprise configuration (e.g., SwiftOnSecurity).
- [ ] Install Splunk Universal Forwarder on `ET-Win11-Target`.
- [ ] Configure the Forwarder to send Windows Event Logs and Sysmon telemetry to the Splunk instance.
- [ ] Verify log ingestion and indexing.

*📸 Screenshot Placeholders:*
> `[Insert Screenshot: Sysmon service running in Windows Services]`
> `[Insert Screenshot: Splunk search head verifying ingestion of logs from ET-Win11-Target]`

---

## ⚔️ Phase 4: Threat Simulation & Detection
**Status:** Pending 🔴

### 🎯 Phase 4 Objectives
- [ ] Simulate a Brute Force authentication attack against the Domain Controller.
- [ ] Execute basic PowerShell-based payloads on the Windows 11 target.
- [ ] Utilize Splunk Search Processing Language (SPL) to hunt for Event IDs related to process creation and registry modifications.
- [ ] Document findings and map to the MITRE ATT&CK framework.

*📸 Screenshot Placeholders:*
> `[Insert Screenshot: Execution of the simulated attack payload in PowerShell]`
> `[Insert Screenshot: Splunk dashboard highlighting the detected malicious activity]`
