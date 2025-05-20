# Assignment--2
Functional &amp; Analytical Test

# Insurance Data Analysis

This project involves preprocessing and analyzing insurance data using basic Python—**without relying on external libraries** like `pandas` or `numpy`. It covers real-world tasks involving data cleaning, visualization, and decision-making based on computed metrics.

## Task 1: Data Preprocessing

### Goal
Clean and prepare raw insurance data from a CSV file using pure Python.

### Process
- The function reads the CSV file line-by-line.
- Handles:
  - Inconsistent or missing values (e.g., `"null"`, `"NA"`, `""`)
  - Invalid or incorrect number formats
- Fills missing values using fallback logic:
  - If `CLAIM_AMOUNT` is missing but `PAID_AMOUNT` is present, it is substituted.
  - If `PAID_AMOUNT` is missing, it is set to `0.0`.
  - If `PREMIUM_COLLECTED` is missing, it is also set to `0.0`.
- The output is a list of cleaned records (Python dictionaries).

### Output
A formatted table of cleaned records is printed using a custom function `print_full_table()`.

## Task 2: City Performance Evaluation

### Goal
Assist XYZ TECH in deciding which city (Pune, Kolkata, Ranchi, or Guwahati) to shut down based on insurance business performance.

### Methodology
- Aggregated key metrics for each city:
  - Total Claim Amount
  - Total Premium Collected
  - Total Paid Amount
- Computed a custom performance **score** per city:
  ```python
  score = (premium_collected - claim_amount - paid_amount)

## Task 3: Rejection Classification

### Goal
Identify the primary reason for claim rejection based on text remarks and label each claim accordingly.

### Approach
- A classification function `complex_rejection_classifier()` was implemented using basic string matching.
- Remarks are categorized into predefined rejection classes:
  - `Fake_document`
  - `Not_Covered`
  - `Policy_expired`
  - If none match, the remark is marked as `Unknown` or `Invalid Remark` based on content.
- The logic is built without using any external NLP or ML tools.

### Error Handling
- All helper functions include exception handling.
- If any unexpected issue occurs during classification, the remark is marked as `"Error"`.

### Integration
- Each record in the cleaned dataset receives a new key `REJECTION_CLASS`, which stores the classification result.
- This is useful for further filtering, analysis, or decision-making.

### Output
A sample set of claims is displayed showing:
- `CLAIM_ID`
- `REJECTION_REMARKS`
- Classified `REJECTION_CLASS`

