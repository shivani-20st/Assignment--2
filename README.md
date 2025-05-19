# Assignment--2
Functional &amp; Analytical Test
# Insurance Claims Data Preprocessing (Core Python)

This project processes an insurance claims dataset using **only core Python** (no pandas, no numpy), and prints the cleaned data in a tabular format.

##  Input

Upload or place the file here:


##  What it does

- Cleans the data: handles `null`, `na`, missing values
- Converts numeric fields like `CLAIM_AMOUNT`, `PAID_AMOUNT`, `PREMIUM_COLLECTED` to `float`
- Fills missing values using logical rules:
  - If `CLAIM_AMOUNT` is missing but `PAID_AMOUNT` exists → copy `PAID_AMOUNT`
  - If `PAID_AMOUNT` is missing but `CLAIM_AMOUNT` exists → set to 0
  - If `PREMIUM_COLLECTED` is missing → set to 0
- Prints the full dataset as a **formatted table** in the notebook output

##  How to Use

Paste this in your Colab or Python file:

```python
from google.colab import drive
drive.mount('/content/drive')

def preprocess_insurance_data(filepath):
    cleaned_data = []
    with open(filepath, 'r') as file:
        headers = file.readline().strip().split(',')
        for line in file:
            row = line.strip().split(',')
            if len(row) != len(headers):
                continue
            data_dict = {}
            for i, value in enumerate(row):
                key = headers[i].strip()
                val = value.strip()
                if val.lower() in ["", "null", "none", "na"]:
                    val = None
                if key.upper() in ['CLAIM_AMOUNT', 'PREMIUM_COLLECTED', 'PAID_AMOUNT'] and val is not None:
                    try:
                        val = float(val)
                    except:
                        val = None
                data_dict[key.upper()] = val
            if data_dict.get('CLAIM_AMOUNT') is None and data_dict.get('PAID_AMOUNT') is not None:
                data_dict['CLAIM_AMOUNT'] = data_dict['PAID_AMOUNT']
            if data_dict.get('PAID_AMOUNT') is None and data_dict.get('CLAIM_AMOUNT') is not None:
                data_dict['PAID_AMOUNT'] = 0.0
            if data_dict.get('PREMIUM_COLLECTED') is None:
                data_dict['PREMIUM_COLLECTED'] = 0.0
            cleaned_data.append(data_dict)
    return cleaned_data

filename = '/content/drive/MyDrive/Insurance_auto_data.csv'
cleaned_data = preprocess_insurance_data(filename)

def print_full_table(data):
    if not data:
        print("No data to display.")
        return
    headers = list(data[0].keys())
    col_widths = [len(header) for header in headers]
    for row in data:
        for i, key in enumerate(headers):
            val = str(row.get(key, ""))
            col_widths[i] = max(col_widths[i], len(val))
    header_row = " | ".join([headers[i].ljust(col_widths[i]) for i in range(len(headers))])
    print(header_row)
    print("-" * len(header_row))
    for row in data:
        row_str = " | ".join([
            str(row.get(key, "")).ljust(col_widths[i]) for i, key in enumerate(headers)
        ])
        print(row_str)

# Run it
print_full_table(cleaned_data)
