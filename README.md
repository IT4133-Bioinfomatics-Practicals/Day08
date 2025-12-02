# 🧬 Day08: Differential Expression Analysis (DEA)

A simple Python notebook for analyzing gene expression differences between control and treatment groups.

---

## 📋 What This Does

Compares gene expression levels between two conditions and identifies which genes are **upregulated**, **downregulated**, or show **no change**.

---

## 🚀 Quick Start

### 1️⃣ Load Data

```python
import pandas as pd
import numpy as np

data = pd.read_csv("dea_data.csv")
data.head()
```

### 2️⃣ Identify Columns

```python
genes = data['Gene']
control_cols = [col for col in data.columns if 'Control' in col]
treatment_cols = [col for col in data.columns if 'Treatment' in col]
```

### 3️⃣ Calculate Means

```python
control_means = data[control_cols].mean(axis=1)
treatment_means = data[treatment_cols].mean(axis=1)
```

### 4️⃣ Compute Fold Change

```python
log2_fc = np.log2(treatment_means / control_means)
```

### 5️⃣ Classify Genes

```python
def classify(fc):
    if fc > 1:
        return "Upregulated"
    elif fc < -1:
        return "Downregulated"
    else:
        return "No Change"

status = log2_fc.apply(classify)
```

### 6️⃣ Create Results Table

```python
dea_results = pd.DataFrame({
    'Gene': genes,
    'Control Mean': control_means.round(2),
    'Treatment Mean': treatment_means.round(2),
    'Log2 Fold Change': log2_fc.round(2),
    'Status': status
})
```

### 7️⃣ Save Results

```python
dea_results.to_csv("dea_results.csv", index=False)
```

---

## 📊 Understanding the Results

| Status           | Meaning                   | Log2 FC |
| ---------------- | ------------------------- | ------- |
| 🔴 Upregulated   | Gene expression increased | > 1     |
| 🔵 Downregulated | Gene expression decreased | < -1    |
| ⚪ No Change     | Gene expression stable    | -1 to 1 |

---

## 📁 Files

- `dea_data.csv` - Input gene expression data
- `dea_results.csv` - Output analysis results
- `Differential_Expression_Analysis.ipynb` - Main notebook

---

## 💡 Key Concepts

- **Mean**: Average expression across replicates
- **Log2 Fold Change**: Measures expression difference (log scale)
- **Threshold**: ±1 log2 FC = 2× change in expression

---

## 🎯 Quick Formula

```
Log2 Fold Change = log2(Treatment Mean / Control Mean)
```

- FC > 1 → Gene goes up 📈
- FC < -1 → Gene goes down 📉
- FC ≈ 0 → No change ➡️

---

_Happy Analyzing! 🧪✨_
