# Use Case 2 – Protecting Finance Data with Microsoft Purview

**Analyst:** Clement C. A. Modebe  
**Program:** Platform Explorers – Cybersecurity  
**Security Platform:** Microsoft Purview  
**Data Protection Solution:** Microsoft Purview Information Protection & DLP  
**Date:** 12 April 2026  

---

## 1. Objective of This Exercise

The objective of this exercise is to:

- Create a **Custom Sensitive Information Type (SIT)** to detect finance identifiers
- Automatically apply **Sensitivity Labels** to emails and files containing finance data
- Restrict **Microsoft 365 Copilot** from processing sensitive finance prompts
- Validate detection, labeling, and enforcement using **simulation and activity logs**
- Document the complete end to end implementation for learning and portfolio purposes

---

## 2. Business Problem Overview

The finance department handles highly sensitive information such as bank account numbers, personal identifiers, and financial records. Unauthorized sharing of this information—either through email, documents, or AI tools like Microsoft 365 Copilot—poses a serious risk of data leakage, compliance violations, and financial loss.

The organization requires a solution that can:
- Automatically classify finance data
- Apply protection consistently
- Prevent AI systems from processing sensitive finance information

---

## 3. Environment Overview

- **Security Platform:** Microsoft Purview  
- **Data Protection Features Used:**
  - Sensitive Information Types (SIT)
  - Sensitivity Labels
  - Auto labeling Policies
  - Data Loss Prevention (DLP) for Microsoft 365 Copilot  
- **Protected Department:** Finance  
- **AI Protection Scope:** Microsoft 365 Copilot (prompt processing)

---

## 4. Technical Implementation

---

### Step 1: Accessing the Microsoft Purview Portal

All configurations were performed in the Microsoft Purview portal, which provides centralized governance, classification, and data protection capabilities.

**Portal:** https://purview.microsoft.com  

**Screenshot Evidence – Microsoft Purview Home**

![Purview Portal Home](Cybersecurity/doc/01_purview_portal-home.png)

*Figure 1: Microsoft Purview portal landing page.*

---

### Step 2: Identifying Finance Data Formats

Before creating detection logic, the finance data formats to be protected were identified.

**Finance Identifiers Selected:**
- Croatian Bank Account Number (IBAN – HR format)
- Nigerian Bank Verification Number (BVN – 11 digits)

**Screenshot Evidence – Detection Planning Notes**

![Detection Formats](Cybersecurity/doc/02_detection-formats_notes.png)

*Figure 2: Finance identifiers selected for classification.*

---

### Step 3: Creating a Custom Sensitive Information Type (SIT)

The organization requires a custom SIT to detect finance identifiers that are not covered by default templates.

**Navigation Path:**  
Information Protection → Classifiers → Sensitive info types

**Screenshot Evidence – Sensitive Info Types List**

![SIT List](Cybersecurity/doc/03_sit_sensitive-info-types_list.png)

---

#### Step 3.1: SIT Name and Description

- **Name:** Finance – Regulated Banking Identifiers (HR IBAN + NG BVN)
- **Description:** Detects Croatian IBAN and Nigerian BVN for finance data protection

**Screenshot Evidence – SIT Creation**

![Create SIT](Cybersecurity/doc/04_sit_create_name-description.png)

---

### Step 4: Adding Detection Patterns

#### Pattern 1: Croatian IBAN

- **Detection Method:** Regular expression
- **Supporting Keywords:** IBAN, Croatia, Hrvatska, Bank account

**Screenshot Evidence – Croatian IBAN Regex**

![HR IBAN Regex](Cybersecurity/doc/05_sit_regex_croatian-iban.png)

**Screenshot Evidence – Croatian IBAN Keywords**

![HR IBAN Keywords](Cybersecurity/doc/06_sit_keywordlist_croatian-iban.png)

**Screenshot Evidence – Pattern Attached**

![HR IBAN Pattern](Cybersecurity/doc/07_sit_supportin-elements_attached_croatian-iban.png)

---

#### Pattern 2: Nigerian BVN

- **Detection Method:** Regular expression (11 digits)
- **Supporting Keywords:** BVN, Bank Verification Number

**Screenshot Evidence – BVN Regex**

![BVN Regex](Cybersecurity/doc/09_sit_regex_primary_nigerian-bvn.png)

**Screenshot Evidence – BVN Keywords**

![BVN Keywords](Cybersecurity/doc/10_sit_keywordlist_nigerian-bvn.png)

---

**Screenshot Evidence – Both Patterns Created**

![Patterns Created](Cybersecurity/doc/12_sit_patterns_page_pattern2-created_nigerian-bvn.png)

---

### Step 5: Reviewing and Creating the SIT

All detection patterns were reviewed before finalizing the SIT.

**Screenshot Evidence – SIT Review**

![SIT Review](Cybersecurity/doc/13_sit_review_page_before-finish.png)

**Screenshot Evidence – SIT Created**

![SIT Created](Cybersecurity/doc/14_sit_creation_page.png)

**Screenshot Evidence – SIT Visible in List**

![SIT List Confirmation](Cybersecurity/doc/15_sit_list_custom-sit-visible.png)

---

## 5. Testing the Sensitive Information Type

A test document containing **fake finance data** was created to validate detection accuracy.

**Screenshot Evidence – Test File Content**

![Test File](Cybersecurity/doc/16_testfile_content_hr-iban_bvn.png)

**Screenshot Evidence – SIT Test Upload**

![Upload Test File](Cybersecurity/doc/17_sit_test_upload_file.png)

**Screenshot Evidence – Detection Results**

![SIT Test Results](Cybersecurity/doc/18_sit_test_results_success.png)

*Figure: Custom SIT successfully detects both IBAN and BVN.*

---

## 6. Creating a Sensitivity Label for Finance Data

A sensitivity label was created to protect files and emails containing finance data.

**Label Name:** Confidential – Finance Restricted

**Screenshot Evidence – Sensitivity Labels Page**

![Labels Page](Cybersecurity/doc/19_label_sensitivity-labels_page.png)

**Screenshot Evidence – Label Basics**

![Label Basics](Cybersecurity/doc/20_label_basics_confidential-finance.png)

---

### Step 6.1: Label Scope

- Files
- Emails

**Screenshot Evidence – Label Scope**

![Label Scope](Cybersecurity/doc/22_label_scope_files-and-emails.png)

---

### Step 6.2: Encryption and Access Control

Access control was configured to restrict access to finance users.

**Screenshot Evidence – Access Control Configuration**

![Access Control](Cybersecurity/doc/25_label_access-control_final-permissions.png)

---

### Step 6.3: Content Marking

A header marking was applied to clearly identify finance-sensitive content.

**Header Text:** CONFIDENTIAL – FINANCE DATA

**Screenshot Evidence – Content Marking**

![Header Marking](Cybersecurity/doc/26_label_content-marking_header-configured.png)

---

### Step 6.4: Label Review and Creation

The label was reviewed and created without publishing manually, as auto labeling would handle enforcement.

**Screenshot Evidence – Label Review**

![Label Review](Cybersecurity/doc/29_label_review_final-summary.png)

**Screenshot Evidence – Label Created**

![Label Created](Cybersecurity/doc/30_label_created_success_dont-publish-yet.png)

---

## 7. Auto Labeling Policy Configuration

An auto labeling policy was created to automatically apply the finance label when the custom SIT is detected.

**Screenshot Evidence – Auto Labeling Policy Page**

![Auto Labeling](Cybersecurity/doc/32_autolabeling_policy_page.png)

**Screenshot Evidence – Policy Type**

![Policy Type](Cybersecurity/doc/33_autolabeling_policy_type_apply-only.png)

**Screenshot Evidence – Custom Info to Label**

![Custom Info](Cybersecurity/doc/34_autolabeling_info-to-label_custom.png)

---

### Step 7.1: Rule Configuration

Condition:
- Content contains Sensitive Info Types
- Custom SIT selected

**Screenshot Evidence – Rule Condition**

![Rule Condition](Cybersecurity/doc/41_autolabeling_rule_condition_custom-sit-selected.png)

---

### Step 7.2: Simulation Mode

The policy was run in simulation mode to validate accuracy before enforcement.

**Screenshot Evidence – Policy Mode**

![Simulation Mode](Cybersecurity/doc/45_autolabeling_policy-mode_simulation.png)

**Screenshot Evidence – Policy Created**

![Auto Label Created](Cybersecurity/doc/47_autolabeling_policy_created_success.png)

---

## 8. DLP Policy for Microsoft 365 Copilot

A DLP policy was created to restrict Microsoft 365 Copilot from processing sensitive finance prompts.

**Action Configured:** Restrict processing prompts (Block)

**Screenshot Evidence – DLP Rule Action**

![Block Copilot](Cybersecurity/doc/59_dlp_rule_action_block_processing-prompts.png)

**Screenshot Evidence – Rule Overview**

![Rule Overview](Cybersecurity/doc/61_dlp_rule_overview_block-copilot-confirmed.png)

---

### Step 8.1: Policy Mode and Deployment

The Copilot DLP policy was deployed in simulation mode with notifications enabled.

**Screenshot Evidence – Policy Mode**

![DLP Simulation](Cybersecurity/doc/62_dlp_policy_mode_simulation_confirmed.png)

**Screenshot Evidence – Policy Created**

![DLP Created](Cybersecurity/doc/64_dlp_policy_created_success.png)

---

## 9. Testing and Validation

### Step 9.1: Copilot Prompt Test

A test prompt containing a fake BVN was submitted to Copilot.

**Screenshot Evidence – Copilot Prompt**

![Copilot Test](Cybersecurity/doc/66_test_copilot_prompt_with-bvn.png)

---

### Step 9.2: Activity Explorer Validation

Detection and policy matches were confirmed in Microsoft Purview Activity Explorer.

**Screenshot Evidence – Activity Explorer**

![Activity Explorer](Cybersecurity/doc/67_dlp_activity-explorer_copilot_sit-detected.png)

---

### Step 9.3: Alert Verification

DLP alerts confirmed successful detection of finance-sensitive prompts.

**Screenshot Evidence – Alerts**

![DLP Alert](Cybersecurity/doc/70_dlp_alert_copilot_bvn.png)

---

## 10. Conclusion

This exercise demonstrates a complete, enterprise grade implementation of finance data protection using Microsoft Purview. By combining custom classification, sensitivity labels, auto labeling, and Copilot DLP controls, the organization effectively reduces the risk of data leakage and unauthorized AI processing of finance information.

