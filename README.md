# Enterprise Security & Threat Hunting Lab

A multi-phase enterprise security lab featuring an isolated Windows 11 target and an Active Directory Domain Controller for threat hunting, telemetry generation, and policy deployment.

## 🧪 Phase 1: Windows 11 Sandbox Provisioning

*Status:* Completed 🟢

## 🎯 Phase 1 Objectives

- [x] Standardize the Windows 11 ISO naming convention.
- [x] Provision a new Hyper-V Virtual Machine (Generation 2) tailored for Windows 11 minimum requirements.
- [x] Configure an isolated "Sandbox" Private Virtual Switch in Hyper-V to prevent accidental network leaks.
- [x] Ensure vTPM and Secure Boot are enabled on the VM hardware for Windows 11 compliance.
- [x] Install Windows 11 using the offline local account bypass (OOBE\BYPASSNRO).
- [x] Establish a clean "Baseline" checkpoint before introducing any tools or threats.

*📸 Screenshots:*

![Hyper-V Virtual Switch Manager showing 'ET-Sandbox' Private Network](Screenshots/ET-Sandbox.png)

![Windows 11 Desktop post-installation (Local Account)](Screenshots/ET-Win11-Target-Desktop.png)

## 🏢 Phase 2: Active Directory Integration

*Status:* Pending 🔴

## 🎯 Phase 2 Objectives

- [ ] Power on ET-DC01 (Windows Server) and connect it to the ET-Sandbox Private Virtual Switch.
- [ ] Configure static IP addressing for both ET-DC01 and ET-Win11-Target.
- [ ] Join ET-Win11-Target to the local Active Directory domain.
- [ ] Create test Organizational Units (OUs) and Domain User accounts.
- [ ] Deploy a Group Policy Object (GPO) to the Windows 11 target (e.g., setting baseline security policies or disabling Defender for testing).

*📸 Screenshot Placeholders:*
[Insert Screenshot: Windows 11 System Properties showing successful Domain Join] 
[Insert Screenshot: Active Directory Users and Computers (ADUC) showing the new ET-Win11-Target machine]

## 🛡️ Phase 3: Telemetry & Log Forwarding

*Status:* Pending 🔴

## 🎯 Phase 3 Objectives

- [ ] Install Sysmon on ET-Win11-Target using an enterprise configuration (e.g., SwiftOnSecurity).
- [ ] Install Splunk Universal Forwarder on ET-Win11-Target.
- [ ] Configure the Forwarder to send Windows Event Logs and Sysmon telemetry to the Splunk instance.
- [ ] Verify log ingestion and indexing.

*📸 Screenshot Placeholders:*
[Insert Screenshot: Sysmon service running in Windows Services] 
[Insert Screenshot: Splunk search head verifying ingestion of logs from ET-Win11-Target]

## ⚔️ Phase 4: Threat Simulation & Detection

*Status:* Pending 🔴

## 🎯 Phase 4 Objectives

- [ ] Simulate a Brute Force authentication attack against the Domain Controller.
- [ ] Execute basic PowerShell-based payloads on the Windows 11 target.
- [ ] Utilize Splunk Search Processing Language (SPL) to hunt for Event IDs related to process creation and registry modifications.
- [ ] Document findings and map to the MITRE ATT&CK framework.

*📸 Screenshot Placeholders:*
[Insert Screenshot: Execution of the simulated attack payload in PowerShell] 
[Insert Screenshot: Splunk dashboard highlighting the detected malicious activity]

## 🧠 Lessons Learned & Troubleshooting

### The Pivot from VirtualBox to Hyper-V
The initial architecture for this lab utilized VirtualBox on a Windows 11 Home host. During the provisioning of the Windows 11 target, severe EFI boot sequence hangs (black screens) and hypervisor conflicts occurred. 

**Root Cause:** Windows 11 Home runs hidden Virtualization-Based Security (VBS) and Core Isolation features that lock the virtualization hardware, forcing VirtualBox into a buggy compatibility mode (often called the "Green Turtle" issue). Furthermore, VirtualBox's graphics/storage controllers struggled to render the WinPE environment for modern Windows 11 ISOs.

**Resolution:** Instead of disabling native Windows security features (Registry/BCD edits) to force VirtualBox to work, the host machine was upgraded to **Windows 11 Pro**. This unlocked Microsoft's native **Hyper-V** hypervisor. Moving the entire lab to Hyper-V resolves the nested virtualization conflicts, securely supports Windows 11 VMs natively, and allows for a more stable, enterprise-grade Private Virtual Switch to route traffic between the Target, DC, and SIEM.
