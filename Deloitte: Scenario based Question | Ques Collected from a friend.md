# 🧮 Scenario: Get Records That Exist Only in Sheet1 (Not in Sheet2)

In this Power BI scenario, we have **two sheets — Sheet1 and Sheet2** — that contain similar columns.  
Our goal is to **create a new table that includes only those records that exist in Sheet1 but not in Sheet2.**

---

## 🗂️ Scenario Overview

There are **two sheets**:
- `Sheet1`
- `Sheet2`

Both sheets contain **6 identical columns**, and some rows are **common between them**.

We need to extract only the **unique records present in Sheet1** (i.e., records *not present in Sheet2*).

<br>

<img width="1919" height="559" alt="Screenshot 2025-10-07 102626" src="https://github.com/user-attachments/assets/fae9f407-d8b7-475c-a27e-53be4065b45a" />
<br>

<img width="1918" height="581" alt="image" src="https://github.com/user-attachments/assets/aa584ef0-4c7d-4d1c-8e60-8168f7aff756" />
<br>

---

## 📊 Practice Dataset

You can view and download the dataset from this Google Sheet:

📄 **[Power BI Scenario Dataset – Sheet1 vs Sheet2](https://docs.google.com/spreadsheets/d/1GN4WUw4B7TLrSWFGxhGw1de-lpLNFvWmxwU8W99Ds7Y/edit?gid=286227172#gid=286227172)**

This Google Sheet contains:
- **Sheet1** → Original records  
- **Sheet2** → Contains some duplicate rows and some new ones

---

## 🧩 Solution 1: Power Query – Merge Queries as New

We can easily achieve this using the **Merge Queries as New** feature in **Power Query**.

### Steps:
1. Load both `Sheet1` and `Sheet2` into Power BI.
2. Go to **Home → Merge Queries → Merge Queries as New**.
3. In the Merge dialog:
   - Select `Sheet1` as the first table.
   - Select `Sheet2` as the second table.
   - Select all six matching columns.
   - Choose **Join Kind = Left Anti (records only in first)**.
4. Click **OK**.
5. A new table will appear — containing only rows from Sheet1 that do not exist in Sheet2.

<br>

<img width="1889" height="965" alt="image" src="https://github.com/user-attachments/assets/f67e5cb8-a2d5-4ce6-acac-f369755a7f28" />
<br>

<img width="1919" height="665" alt="image" src="https://github.com/user-attachments/assets/357af504-6fdf-4028-97f7-5013a690bafd" />
<br>

✅ **Result:** You’ll get only the rows that are unique to `Sheet1`.

---

## 🧩 Solution 2: Using DAX

Alternatively, you can use a **DAX expression** to create a new calculated table.

### Steps:
1. Go to **Modeling → New Table**
2. Write the following DAX code:

```dax
OnlyInSheet1 =
EXCEPT(
    Sheet1,
    Sheet2
)
````

### Explanation:

* The **`EXCEPT()`** function returns the rows that exist in the first table but not in the second.
* Here, it compares all columns automatically (since both tables have the same structure).

<br>

<img width="1094" height="463" alt="image" src="https://github.com/user-attachments/assets/b955c25d-4c4a-47f2-bafd-3ece587ac7c9" />
<br>

✅ **Result:** You’ll get a new table (`OnlyInSheet1`) containing only those records that exist in `Sheet1` and not in `Sheet2`.

---

## 🧠 Key Learning

| Method                                 | Description                                                                   | Output Table         |
| -------------------------------------- | ----------------------------------------------------------------------------- | -------------------- |
| **Power Query Merge (Left Anti Join)** | Uses GUI to compare two sheets and return non-matching rows                   | New Query            |
| **DAX EXCEPT()**                       | Formula-based method to return records present in one table but not the other | New Calculated Table |

Both methods produce the same result — choose based on your workflow preference:

* Use **Power Query** if you’re cleaning or transforming data.
* Use **DAX** if you’re modeling or analyzing data within Power BI.

---

## 📽️ Reference

🎥 [YouTube Video: Power BI Scenario – Find Records Only in One Sheet | DAX vs Power Query](https://youtu.be/MoaDV9b5NAc?si=5l0ATLWzdaLYv_k3)

📺 Channel: *LearnWidGiggs*

---

### ✍️ Author’s Note

This question is a **real-world Power BI interview scenario**, frequently asked by Deloitte and similar companies.
It tests your understanding of **joins, data transformation**, and **DAX set functions** like `EXCEPT()`.



