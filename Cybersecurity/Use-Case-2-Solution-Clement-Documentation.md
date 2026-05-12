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

**Portal:** https://purview.microsoft.com  

![Purview Portal Home](doc/01_purview_portal-home.png)

*Figure 1: Microsoft Purview portal landing page.*

---

### Step 2: Identifying Finance Data Formats

**Finance Identifiers Selected:**
- Croatian Bank Account Number (IBAN – HR format)
- Nigerian Bank Verification Number (BVN – 11 digits)

![Detection Formats](doc/02_detection-formats_notes.png)

*Figure 2: Finance identifiers selected for classification.*

---

### Step 3: Creating a Custom Sensitive Information Type (SIT)

![SIT List](doc/03_sit_sensitive-info-types_list.png)

---

#### Step 3.1: SIT Name and Description

![Create SIT](doc/04_sit_create_name-description.png)

---

### Step 4: Adding Detection Patterns

#### Pattern 1: Croatian IBAN

![HR IBAN Regex](doc/05_sit_regex_croatian-iban.png)

![HR IBAN Keywords](doc/06_sit_keywordlist_croatian-iban.png)

![HR IBAN Pattern](doc/07_sit_supportin-elements_attached_croatian-iban.png)

---

#### Pattern 2: Nigerian BVN

![BVN Regex](doc/09_sit_regex_primary_nigerian-bvn.png)

![BVN Keywords](doc/10_sit_keywordlist_nigerian-bvn.png)

![Patterns Created](doc/12_sit_patterns_page_pattern2-created_nigerian-bvn.png)

---

### Step 5: Reviewing and Creating the SIT

![SIT Review](doc/13_sit_review_page_before-finish.png)

![SIT Created](doc/14_sit_creation_page.png)

![SIT List Confirmation](doc/15_sit_list_custom-sit-visible.png)

---

## 5. Testing the Sensitive Information Type

![Test File](doc/16_testfile_content_hr-iban_bvn.png)

![Upload Test File](doc/17_sit_test_upload_file.png)

![SIT Test Results](doc/18_sit_test_results_success.png)

---

## 6. Creating a Sensitivity Label for Finance Data

![Labels Page](doc/19_label_sensitivity-labels_page.png)

![Label Basics](doc/20_label_basics_confidential-finance.png)

---

### Step 6.1: Label Scope

![Label Scope](doc/22_label_scope_files-and-emails.png)

---

### Step 6.2: Encryption and Access Control

![Access Control](doc/25_label_access-control_final-permissions.png)

---

### Step 6.3: Content Marking

![Header Marking](doc/26_label_content-marking_header-configured.png)

---

### Step 6.4: Label Review and Creation

![Label Review](doc/29_label_review_final-summary.png)

![Label Created](doc/30_label_created_success_dont-publish-yet.png)

---

## 7. Auto Labeling Policy Configuration

![Auto Labeling](doc/32_autolabeling_policy_page.png)

![Policy Type](doc/33_autolabeling_policy_type_apply-only.png)

![Custom Info](doc/34_autolabeling_info-to-label_custom.png)

---

### Step 7.1: Rule Configuration

![Rule Condition](doc/41_autolabeling_rule_condition_custom-sit-selected.png)

---

### Step 7.2: Simulation Mode

![Simulation Mode](doc/45_autolabeling_policy-mode_simulation.png)

![Auto Label Created](doc/47_autolabeling_policy_created_success.png)

---

## 8. DLP Policy for Microsoft 365 Copilot

![Block Copilot](doc/59_dlp_rule_action_block_processing-prompts.png)

![Rule Overview](doc/61_dlp_rule_overview_block-copilot-confirmed.png)

---

### Step 8.1: Policy Mode and Deployment

![DLP Simulation](doc/62_dlp_policy_mode_simulation_confirmed.png)

![DLP Created](doc/64_dlp_policy_created_success.png)

---

## 9. Testing and Validation

### Step 9.1: Copilot Prompt Test

![Copilot Test](doc/66_test_copilot_prompt_with-bvn.png)

---

### Step 9.2: Activity Explorer Validation

![Activity Explorer](doc/67_dlp_activity-explorer_copilot_sit-detected.png)

---

### Step 9.3: Alert Verification

![DLP Alert](doc/70_dlp_alert_copilot_bvn.png)

---

## 10. Conclusion

This exercise demonstrates a complete, enterprise grade implementation of finance data protection using Microsoft Purview. By combining custom classification, sensitivity labels, auto labeling, and Copilot DLP controls, the organization effectively reduces the risk of data leakage and unauthorized AI processing of finance information.
