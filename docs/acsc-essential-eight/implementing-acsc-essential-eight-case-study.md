From Assessment to Remediation: Implementing the ACSC Essential Eight in a Real Environment


In August 2024, I initiated and completed a comprehensive assessment against the Australian Cyber Security Centre Essential Eight framework to identify security gaps and improvement opportunities.

Since then, I have been leading in ongoing remediation efforts to strengthen security controls across. This project has provided interesting practical experience for me.

Environment and Scope of Assessment:
- Medium-sized organization
- Target: Maturity level 1
- Microsoft 365 cloud-first
- On-prem network devices and third-party applications
- Microsoft Intune endpoint management

I was a system administrator (outsource), I started with researching information from ASD website below:
https://www.cyber.gov.au/business-government/asds-cyber-security-frameworks/essential-eight

I went through the assessment process guide, accumulate the assessment guidance information to **create a comprehensive checklist (excel file)**. Since, I started looking after this organisation in mid 2024, I came across that they did not have asset and inventory register, therefore, I **initiated the simple asset management process, and created the register** using Microsoft List which is an app in MS365. I have spent a couple of months to collect necessary asset details. Additionally, I **create the list of standard user accounts and privilege users** in MS365, Network devices, and third-party web application that the organisation have used.

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

![MFA Conditional Access Policy](https://github.com/Penguinsecq/penguinsecq.github.io/raw/main/docs/images/cap-mfa1.png)

However, a couple of users still need to be excluded because of a requirement and a bit technical constraints. To mitigate the risk of not having MFA enabled for the accounts, after excluding them from the MFA policy. The followings condition could be applied depending on your environment:

**Mitigation**
-Device compliant  
-Location filtering such as ip address  
-Device ID filtering but device registering is required  

With the filtering above, risk is mitigated.
