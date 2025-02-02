# Data Investigation Report

## **Overview**
This document summarizes the findings from our exploratory data analysis (EDA) of user, transaction, and product data. It highlights key **data quality issues**, **interesting trends**, **outstanding questions**, and **assumptions** made during the investigation.

## **Data Quality Issues**
### **Users Table**
- **Missing Values**:
  - `BIRTH_DATE`: 3,675 missing (impacting age-based analysis).
  - `STATE`: 4,812 missing (affects geographic insights).
  - `LANGUAGE`: 30,508 missing (limits localization and language-based personalization).
  - `GENDER`: 5,892 missing (affects gender segmentation).

### **Transactions Table**
- **Missing Values**:
  - `BARCODE`: 5,762 missing (prevents mapping transactions to specific products).
  - `FINAL_SALE`: 12,500 missing (may indicate refunds, free products, or system errors).

### **Products Table**
- **Brand Data Issues**:
  - 226,472 records have missing `BRAND`.
  - `BRAND NOT KNOWN` and `PRIVATE LABEL` are used as placeholders, limiting brand-level insights.
  - Top brands like **CVS, SEGO, MEIJER, DOVE, RITE AID** are present but have incomplete coverage.

## **Interesting Trends**
### **User Demographics**
- The majority of users identify as **female (64,240 users)**, followed by **male (25,829 users)**.
- A significant portion of users identify as **non_binary, transgender, prefer_not_to_say, or other self-defined categories**, suggesting an opportunity for **inclusive experiences**.
  
### **Sales & Transactions**
- **Some states have high transaction volumes**, but due to **missing state data**, regional analysis is **not fully reliable**.
- **Missing barcode values** prevent detailed product analysis for a portion of transactions.

## **Assumptions**
### **Handling Missing Data**
1. **Users Table**:
   - If `STATE` is missing, we assume users might have entered incomplete profiles or moved. Defaulting these to "Unknown" is one approach.
   - If `LANGUAGE` is missing, we assume users may have defaulted to English or the primary language in their region.
   - If `BIRTH_DATE` is missing, we cannot accurately estimate user age, which limits cohort analysis.

2. **Transactions Table**:
   - If `FINAL_SALE` is missing, we assume it could be a **non-revenue transaction** (e.g., refunds, system issues, free products).
   - If `BARCODE` is missing, we assume these transactions are either **miscategorized products** or involve products outside our tracking system.

3. **Products Table**:
   - "BRAND NOT KNOWN" and "PRIVATE LABEL" might refer to **generic, store-brand, or unregistered** products.
   - Missing `BRAND` data means we **cannot** conduct brand-level trend analysis for those items.

## **Outstanding Questions**
### **Users**
1. Should missing `STATE` values be labeled as "Unknown," or is further validation required?
2. Should we assume missing `LANGUAGE` values default to English, or should we infer based on region?

### **Transactions**
3. Are missing `FINAL_SALE` values considered refunds, system issues, or valid zero-dollar transactions?
4. Can transactions with missing `BARCODE` still be linked to products via another dataset?

### **Products**
5. Do we have an external source to improve brand classification?
6. Should "BRAND NOT KNOWN" and "PRIVATE LABEL" be included in brand-level reports, or should they be filtered out?

## **Next Steps**
1. **Data Cleaning**: Address missing values where possible.
2. **Validation**: Confirm product-brand associations with the business team.
3. **Further Analysis**: Investigate missing sales values to determine their business implications.

---
