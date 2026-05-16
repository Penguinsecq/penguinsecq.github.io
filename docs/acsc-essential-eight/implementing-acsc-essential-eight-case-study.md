From Assessment to Remediation: Implementing the ACSC Essential Eight in a Real Environment


In August 2024, I initiated and completed a comprehensive assessment against the Australian Cyber Security Centre Essential Eight framework to identify security gaps and improvement opportunities.

Since then, I have been leading in ongoing remediation efforts to strengthen security controls across. This project has provided interesting practical experience for me.

Environment and Scope of Assessment:
- Medium-sized organization
- Target: Maturity level 1
- Microsoft 365 cloud-first
- On-prem network devices
- Third-party applications
- Microsoft Intune endpoint management

I am not focusing about Windows platform only, I wanted to take this opportunity to improve this organisation cybersecurity posture in overall, and wanted to initiate the cybersecurity standard for them, and my team members who also were the outsource staffs because I found that their system can be improved. If you follow this article to the end, you will see a lot of Information security policy and documents were created for the client.

Background, I was both a system administrator and security (outsource), I started with researching information from ASD website below:
https://www.cyber.gov.au/business-government/asds-cyber-security-frameworks/essential-eight

I went through the assessment process guide, accumulate the assessment guidance information to **create a comprehensive checklist (excel file)**. Since, I started looking after this organisation in mid 2024, I came across that they did not have asset and inventory register, therefore, I **initiated the simple asset management process, and created the asset register** using Microsoft List which is an app in MS365. I have spent a couple of months to collect necessary asset details. Additionally, I **create the list of standard user accounts and privilege users** in MS365, Network devices, and third-party web application that the organisation have used.

I started conducting the assessment on all in-scoped system by 
- Reviewing the existence of processes,
- Reviewing the effectiveness of controls, configuration
- Reviewing relevant documents and reports,
- Vulnerability scanning
- Interviewing and surveys.
- etc.

Any assessment evidences, limitataions, screenshots and constraints on testing were documented within the finding summary report. I sent the detaild finding report with executive summary to the client. The followings are the implementation challenges that I want to keep and share as valuable experience. Hope, it might be useful.

**Case study 1 - Multi-factor authentication issue**
I found that MFA is not enforced for all some users. I created conditional access policy to enforce all users to be required the MFA. 

<div align="center">
<img src="https://github.com/Penguinsecq/penguinsecq.github.io/raw/main/docs/images/cap-mfa1.png" alt="MFA Conditional Access Policy" style="border: 1px solid grey;">
</div><br>

However, a couple of users still need to be excluded because of a requirement and a bit technical constraints. To mitigate the risk of not having MFA enabled for the accounts, after excluding them from the MFA policy. The followings condition could be applied depending on your environment:

**Mitigation**<br>
-Device compliant<br>
-Location filtering such as ip address<br>
-Device ID filtering but device registering is required<br>
<div align="center">
<img src="https://github.com/Penguinsecq/penguinsecq.github.io/raw/main/docs/images/cap-device-filter.png" alt="Device filter in Conditional access policy" style="border: 1px solid grey;">
</div><br>

With the filterings above, risk is mitigated.<br>

**Case study 2 - Restrict Admin Privilege issue**

There is no documented and approved list of privileged accounts, processes and procedures that outline the requirements for provisioning privileged accounts. Also, a privileged MS365 users have accessed some users’ workstation, also there is a usage of privileged user to do daily routine operation.

This is why the asset register, third-party application and user accounts list are required at the beginning of the assessment, you need to know
- How many system (Windows, Network devices, Applications
- How many User accounts both standard and privileged,
- Where the privileged user to be used,
- which systems got accessed by the privileged user (I will talk about this in next article)

**Implementation**<br>
- Create Privilege Access Request Procedure and document.
- I used Microsoft Forms to create a Privilege access request form. Actually, you can utilise the Privilege Access Management in MS365 for this issue if you have a required license (Microsoft 365 E5 (no Teams), Office 365 E5, Microsoft 365 F5).
- Remove all local administrator user.
- After reviewing, remove unnecessary MS365 administrative users. 
- Create new user for Intune enrollment only, not Global admin anymore.
- Create policy to prohibit MS365 global admin user to access or logon to any Entra joined workstation

<div align="center">
<img src="https://github.com/Penguinsecq/penguinsecq.github.io/raw/main/docs/images/pam-procedures.png" alt="Privilege Access Management process" style="border: 1px solid grey;"><br>
  Privilege Access Request Procedures flow. Generated by Claude AI. I am lazy, sorry.
</div><br>

**Case study 3 - Application Control issue**

This section is the most challenging for me to accomplish the Essential 8 Maturity Level 1, even though I have a implementation plan because client's environment always is different. One of my client, they have many branches and they are in the middle of nowhere. If the application control do something wrong for example block "dll", "exe" or other file extensions which are necessary for the operating system. Windows will be crashed, and even though with the approval from the client, It's not a good idea. 

**Implementation**<br>

Monitor Event Logs:
Check Event Viewer > Applications and Services Logs > Microsoft > Windows > AppLocker for Event ID 8004 (audit log of blocked executions).

Review Audit Results:
Identify which executables, scripts, installers, or packaged apps would be blocked if enforcement were enabled.

Document Allowed Applications:
Create a list of legitimate applications flagged during the audit for future whitelisting.

Refine Rules:
Update AppLocker rules to include any necessary exceptions or allow rules for trusted apps, vendors, or paths.

Test on Pilot Devices:
Apply refined policies to a small group of users or machines to confirm no legitimate software is impacted.

Repeat Audit Cycle:
Continue auditing and refining policies until no valid applications are reported as blocked.

Educate Users:
Inform staff of the upcoming changes, and provide a process for requesting access to blocked apps.

Plan for Enforcement:
Once confident in the rules, gradually move from audit to enforced mode using staged deployment.

Backup Policies:
Export and save a copy of your final AppLocker policies for rollback or documentation.

Enable Enforcement (Final Step):
Switch AppLocker from Audit Mode to Enforced Mode only after validating all business-critical apps are allowed.




