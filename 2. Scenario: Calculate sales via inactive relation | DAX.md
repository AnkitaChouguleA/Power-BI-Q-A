# 💡 Power BI DAX: Calculate Total Sales or Revenue Using an Inactive Relationship

In Power BI, when multiple relationships exist between two tables (for example, `OrderDate` and `StockDate`), only one can be **active**.  
To calculate measures using an **inactive relationship**, we use the powerful `USERELATIONSHIP()` function.

---

## 🔗 Scenario Overview

There is:
- **Active relationship** between `Date` column and `OrderDate` column  
  <br>
  <img width="1919" height="976" alt="image" src="https://github.com/user-attachments/assets/ac2a2f65-f3eb-4e99-a5fe-b0f754f21e68" />
  <br>

- **Inactive relationship** between `Date` column and `StockDate` column  
  <br>
  <img width="1915" height="939" alt="image" src="https://github.com/user-attachments/assets/e1008fee-8f61-489f-add3-bcc4eadc97d9" />
  <br>

Now we will calculate **Total Sales** using this **inactive relationship**.

---

## ⚙️ About `USERELATIONSHIP()`

The `USERELATIONSHIP()` function in DAX is used to temporarily **activate an existing inactive relationship** between two tables for a specific calculation.

### 🧠 Key Aspects

- **Purpose:** Activates an existing *inactive* relationship for a calculation  
- **Use Case:** When multiple relationships exist between two tables (e.g., Sales ↔ Date with both OrderDate and ShipDate)
- **Syntax:**
  ```dax
  USERELATIONSHIP ( <ColumnName1>, <ColumnName2> )

- **Used Inside:** CALCULATE(), CALCULATETABLE(), or time intelligence functions

- **Temporary Effect:** Applies only to the current measure; doesn’t change the model

- **Common in:** Role-playing dimensions (Order Date, Ship Date, Delivery Date, etc.)
  
- **Usage with CALCULATE:** It is commonly used as a modifier within the CALCULATE function to change the filter context based on a different relationship. 
    ```dax
    CALCULATE (
        [Total Sales],
        USERELATIONSHIP ( Sales[Ship Date], 'Date'[Date] )
    )

Here, Total Sales would be calculated based on the 'Ship Date' instead of the default active relationship (e.g., 'Order Date'). 

- **Temporary effect:** The effect of USERELATIONSHIP is temporary and applies only to the specific DAX expression in which it is used. After the calculation is complete, the default active relationship between the tables is restored. 

- **Role-playing dimensions:** This function is particularly useful when dealing with role-playing dimensions, where a single dimension table (like a Date table) is used in multiple roles with a fact table (e.g., for order date, ship date, delivery date, etc.). 

<br></br>
<img width="1910" height="883" alt="image" src="https://github.com/user-attachments/assets/3306aa6c-4228-4e3a-a01c-56e7515c0cb0" />
<br></br>

<img width="566" height="413" alt="image" src="https://github.com/user-attachments/assets/8fc31caf-480e-4b37-98b9-19586dbacb07" />
<br></br>


## 🧩 Practice It Yourself in Power BI

If you want to try the **`USERELATIONSHIP()`** concept hands-on, follow these steps to build the same scenario shown in the video — even if you don’t have the original dataset.

---

### 🗂️ 1. Download Practice Dataset

You can download the Excel file here:
📂 [PowerBI_InactiveRelationship_Practice.xlsx](https://github.com/user-attachments/files/22736391/PowerBI_InactiveRelationship_Practice.xlsx)

This Excel file contains two sheets:
* **Sales** → includes `OrderDate`, `StockDate`, and `Revenue`
* **Calendar** → contains dates for January 2024

---

### 🧱 2. Load the Data into Power BI

1. Open **Power BI Desktop**
2. Go to **Home → Get Data → Excel**
3. Load both tables: `Sales` and `Calendar`
4. Confirm they appear in the **Fields Pane**

---

### 🔗 3. Create Active and Inactive Relationships

Go to **Model View** and connect:

* **Active Relationship** → `Calendar[Date]` → `Sales[OrderDate]` (solid line)
* **Inactive Relationship** → `Calendar[Date]` → `Sales[StockDate]` (dotted line)

✅ Active: Calendar[Date] — Sales[OrderDate]

❌ Inactive: Calendar[Date] — Sales[StockDate]

---

### ⚙️ 4. Create the Measures

```dax
Total Revenue = SUM(Sales[Revenue])
```

```dax
Total Revenue by Stock Date =
CALCULATE(
    [Total Revenue],
    USERELATIONSHIP(
        Calendar[Date],
        Sales[StockDate]
    )
)
```
🧱 Data Model View

The below diagram shows how both relationships exist between Calendar and Sales tables:

Solid line → Active relationship (OrderDate)

Dotted line → Inactive relationship (StockDate)

<img width="1129" height="751" alt="Screenshot 2025-10-07 121158" src="https://github.com/user-attachments/assets/42997ccb-e52c-4f14-8918-dc864046d732" />

---

### 📊 5. Visualize the Result

Add a **Table visual** in Report View and include:

* `Calendar[Date]`
* `[Total Revenue]`
* `[Total Revenue by Stock Date]`

### 🖼️ Power BI Result Preview

The below report shows both measures — `Total Revenue` (active relationship) and  
`Total Revenue by Stock Date` (using `USERELATIONSHIP()` with inactive relationship):

<img width="1910" height="991" alt="image" src="https://github.com/user-attachments/assets/370f7155-c250-4285-b593-ab16a8b4158a" />


> Both visuals show **3200**, confirming that the inactive relationship was activated correctly by the DAX measure.


You’ll see that:

* `Total Revenue` uses the **active** relationship (Order Date)
* `Total Revenue by Stock Date` uses the **inactive** one activated by `USERELATIONSHIP()`

---

### ✅ Verification Tip

To confirm the inactive relationship is working:

1. Temporarily deactivate the **active relationship** (`OrderDate`) in Model View
2. Refresh your visuals
3. Only `[Total Revenue by Stock Date]` should return values

This confirms that `USERELATIONSHIP()` successfully used the inactive path.

---

## 🧠 Key Learnings

* Power BI allows **only one active relationship** between two tables.
* Use `USERELATIONSHIP()` to **temporarily activate** another (inactive) one.
* It’s essential for **role-playing dimension** scenarios like:

  * Order Date vs. Ship Date
  * Invoice Date vs. Payment Date
  * Created Date vs. Closed Date

---

## 📽️ Reference

🎥 [YouTube Video: Scenario - Calculate Sales via Inactive Relation | DAX | Power BI Interview 🔥](https://www.youtube.com/watch?v=JBYQKksIAKc)

📺 Channel: *LearnWidGiggs*

---

### ✍️ Author’s Note

This walkthrough helps you practice the `USERELATIONSHIP()` function without needing the original dataset.
It’s a must-know DAX concept for Power BI developers, especially for interview and project scenarios!
