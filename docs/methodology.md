# SOC Investigation Methodology  
**BOTSv3 – Splunk-Based Incident Analysis**

---

## 1. Investigation Approach

This investigation follows a **SOC-aligned, evidence-driven methodology** designed to replicate real-world Security Operations Centre (SOC) workflows. Instead of treating each BOTSv3 question as an isolated task, the analysis applies structured log correlation across multiple data sources to identify and validate security-relevant events.

The methodology is informed by:
- SOC Tier 2 analyst responsibilities
- Incident handling lifecycle best practices
- Cloud and endpoint security monitoring principles

This ensures that findings are contextual, defensible, and operationally relevant.

---

## 2. SOC-Aligned Investigation Framework

The investigation aligns with the standard **incident handling lifecycle** commonly adopted in professional SOC environments.

### 2.1 Detection

Detection focuses on identifying anomalous or high-risk activity within the environment. In this investigation, detection was driven by:

- Keyword-based searches (e.g. `PutBucketAcl`, `REST.PUT.OBJECT`)
- Authentication context analysis (e.g. MFA usage)
- Baseline comparison across hosts and user accounts

Primary Splunk sourcetypes used during detection:
- `aws:cloudtrail`
- `aws:s3:accesslogs`
- `operatingsystem`
- `hardware`

---

### 2.2 Analysis

Once potential security events were detected, deeper analysis was conducted to determine:

- **Who** performed the action (identity attribution)
- **What** resource was affected (S3 bucket, file, host)
- **How** the activity was executed (API calls, ACL changes)
- **Whether** the behaviour aligned with security best practices

Splunk Search Processing Language (SPL) was used extensively for:
- Field extraction
- Aggregation and correlation
- Validation of event success or failure

This reflects Tier 2 SOC workflows where analysts validate alerts prior to escalation.

---

### 2.3 Response Considerations

Although BOTSv3 is a simulated dataset, response actions were considered to reflect realistic SOC decision-making. Identified issues included:

- Publicly accessible S3 bucket misconfiguration
- AWS API activity performed without MFA
- Object uploads during periods of public exposure

In a live SOC environment, these findings would typically result in:
- Cloud security alerts
- Immediate configuration remediation
- IAM policy and access reviews

---

### 2.4 Recovery and Lessons Learned

The recovery phase focuses on learning and improvement rather than remediation. Each incident finding was reviewed to determine:

- Which security controls failed or were misconfigured
- How detection rules could be improved
- What preventative controls could reduce future risk

This phase supports continuous improvement, a key characteristic of mature SOC operations.

---

## 3. Data Sources and Validation

The investigation utilised multiple data sources within the BOTSv3 dataset:

| Data Source | Purpose |
|------------|--------|
| `aws:cloudtrail` | Cloud API activity and identity attribution |
| `aws:s3:accesslogs` | Object-level S3 access validation |
| `operatingsystem` | Endpoint OS identification |
| `hardware` | Infrastructure and CPU baseline analysis |

Each data source was validated after ingestion by:
- Confirming expected event volume
- Verifying critical fields
- Testing known example queries

This ensured confidence in all subsequent analysis.

---

## 4. Splunk Query Development Process

Splunk queries were developed iteratively using the following approach:

1. Broad searches to identify relevant events
2. Field extraction using `spath` where required
3. Filtering and aggregation using `stats`, `table`, and `where`
4. Query refinement for accuracy and clarity
5. Documentation and evidence capture

This mirrors professional SOC investigation practices, where queries evolve throughout the investigation.

---

## 5. Evidence Handling

Evidence was preserved and presented through:
- Saved SPL queries (`queries/` directory)
- Screenshots of query outputs (`screenshots/`)
- Written justification within the report

This ensures all conclusions are traceable to raw log data, meeting both academic and professional standards.

---

## 6. Methodology Limitations

Several limitations are acknowledged within this methodology:

- The BOTSv3 dataset is static and does not reflect real-time SOC monitoring
- No automated alerting or SOAR integration is present
- External threat intelligence enrichment is unavailable

These limitations are inherent to the dataset and do not detract from the investigative objectives.

---

## 7. SOC Relevance Summary

This methodology demonstrates:
- Practical SOC investigation skills
- Effective use of Splunk for cloud and endpoint analysis
- Alignment with real-world incident handling frameworks

The approach reflects industry practices and supports both academic assessment and professional SOC readiness.
