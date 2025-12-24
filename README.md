# COMP3010 – SOC Monitoring Analysis using BOTSv3

**Student Name:** Mohammed Nasser Alsultan  
**Student ID:**  
**University:** University of Plymouth  
**Module:** COMP3010  

---

## 1. Introduction

This report documents a Security Operations Centre (SOC) monitoring-focused investigation
using the Boss of the SOC v3 (BOTSv3) dataset within Splunk Enterprise. BOTSv3 simulates
a realistic security incident within a fictitious organisation, Frothly, providing diverse
log sources including AWS CloudTrail, S3 access logs, and endpoint telemetry.

The objective of this investigation is to demonstrate how a SOC analyst can design,
execute, and evaluate detection logic to identify security-relevant events, misconfigurations,
and anomalous behaviour within a monitored environment.

Unlike a purely forensic investigation, this report emphasises continuous monitoring,
alert relevance, and escalation considerations aligned with real-world SOC operations.

---

## 2. SOC Roles & Incident Handling Reflection

Within a SOC environment, responsibilities are commonly divided across tiers.
Tier 1 analysts focus on alert triage and validation, Tier 2 analysts conduct deeper
investigations, and Tier 3 analysts handle advanced threat hunting and response.

The BOTSv3 exercise closely aligns with Tier 2 SOC responsibilities. The analysis
demonstrates how detection outputs from AWS and endpoint telemetry can support
incident identification, prioritisation, and escalation.

Incident handling phases reflected in this investigation include:
- **Detection:** Identifying anomalous or risky activity such as public S3 buckets
  and API usage without MFA.
- **Analysis:** Correlating user activity, event metadata, and system context.
- **Response:** Highlighting misconfigurations requiring remediation.
- **Recovery:** Informing long-term monitoring improvements.

---

## 3. Installation & Data Preparation

Splunk Enterprise was deployed on an Ubuntu virtual machine to simulate a SOC monitoring
platform. The BOTSv3 dataset was ingested using Splunk’s pre-indexed format to ensure
data integrity and consistent analysis.

Key validation steps included:
- Verification of the `botsv3` index
- Confirmation of AWS and endpoint sourcetypes
- Sampling of events across CloudTrail, S3, and WinHostMon sources

This configuration reflects a typical SOC deployment where cloud and endpoint telemetry
is centralised for correlation and alerting.

---

## 4. Guided Questions – BOTSv3 (200-Level)

### Q1 – IAM Users Accessing AWS Services
IAM users accessing AWS services were identified using CloudTrail logs.
This supports SOC visibility into both successful and unsuccessful access attempts.

**Result:**  
`bstoll, btun, splunk_access, web_admin`

---

### Q2 – Detecting AWS API Activity Without MFA
The CloudTrail field used to detect API activity without MFA is:

**Result:**
`userIdentity.sessionContext.attributes.mfaAuthenticated`


This field is critical for SOC alerting, enabling detection of weak authentication
practices.

---

### Q3 – Processor Used on Web Servers
Hardware telemetry was analysed to identify processor details on web servers.

**Result:**  
`Intel(R) Xeon(R) CPU E5-2676`

---

### Q4 – Public S3 Bucket Misconfiguration Event ID
An S3 bucket was made publicly accessible via a `PutBucketAcl` API call.

**Event ID:**  
`ab45689d-69cd-41e7-8705-5350402cf7ac`

---

### Q5 – Bud’s Username
Console login activity revealed Bud’s IAM username.

**Result:**  
`bstoll`

---

### Q6 – Publicly Accessible S3 Bucket Name
The S3 bucket affected by the misconfiguration was identified.

**Result:**  
`frothlywebcode`

---

### Q7 – Text File Uploaded to the Public S3 Bucket
S3 access logs were analysed to identify successful object uploads.

**Result:**  
`OPEN_BUCKET_PLEASE_FIX.txt`

---

### Q8 – Endpoint with Different Windows OS Edition
Endpoint telemetry was analysed to identify an outlier operating system.

**Result:**  
`BSTOLL-L`

---

## 5. Conclusion

This investigation demonstrates how SOC monitoring techniques can be applied to
identify cloud misconfigurations, authentication weaknesses, and endpoint anomalies.
The BOTSv3 dataset provides a realistic environment to practice detection logic,
log correlation, and SOC decision-making.

Future improvements could include automated alert thresholds, dashboards, and
integration with incident response workflows to enhance detection efficiency.

---

## References

[1] Splunk, *Boss of the SOC v3 Dataset*, https://github.com/splunk/botsv3  
[2] Amazon Web Services, *AWS CloudTrail Documentation*, https://docs.aws.amazon.com/cloudtrail  
[3] Amazon Web Services, *Amazon S3 API Reference*, https://docs.aws.amazon.com/AmazonS3  
