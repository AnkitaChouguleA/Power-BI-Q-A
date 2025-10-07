Calculate Total sales or Revenue using inactive relation between dim and fact table.

There is active relationship between Date col and OrderDate col
<br></br>
<img width="1919" height="976" alt="image" src="https://github.com/user-attachments/assets/ac2a2f65-f3eb-4e99-a5fe-b0f754f21e68" />
<br></br>
There is inactive relationship between Date col and StockDate col
<br></br>
<img width="1915" height="939" alt="image" src="https://github.com/user-attachments/assets/e1008fee-8f61-489f-add3-bcc4eadc97d9" />
<br></br>
Now we have to calculate sale using this inactive relatonship. We will use 'USERELATIONSHIP' function to create this measure. 
The USERELATIONSHIP function in DAX is used to specify an existing, potentially inactive, relationship between two tables to be used for the duration of a specific DAX expression. It is primarily used within other functions that accept a filter argument, such as CALCULATE, CALCULATETABLE, and time intelligence functions. 

Key aspects of USERELATIONSHIP: 

• Activating inactive relationships: When multiple relationships exist between two tables (e.g., a Sales table and a Date table with both 'Order Date' and 'Ship Date'), only one can be active by default. USERELATIONSHIP allows you to temporarily activate an inactive relationship for a particular calculation without changing the data model's default active relationship. 

• Syntax: The function takes two arguments: the two columns that define the relationship you want to activate. The order of the columns is not important. [1]  

    USERELATIONSHIP ( <ColumnName1>, <ColumnName2> )

• Usage with CALCULATE: It is commonly used as a modifier within the CALCULATE function to change the filter context based on a different relationship. 

    CALCULATE (
        [Total Sales],
        USERELATIONSHIP ( Sales[Ship Date], 'Date'[Date] )
    )

In this example, Total Sales would be calculated based on the 'Ship Date' instead of the default active relationship (e.g., 'Order Date'). 

• Temporary effect: The effect of USERELATIONSHIP is temporary and applies only to the specific DAX expression in which it is used. After the calculation is complete, the default active relationship between the tables is restored. 

• Role-playing dimensions: This function is particularly useful when dealing with role-playing dimensions, where a single dimension table (like a Date table) is used in multiple roles with a fact table (e.g., for order date, ship date, delivery date, etc.). 

<br></br>
<img width="1910" height="883" alt="image" src="https://github.com/user-attachments/assets/3306aa6c-4228-4e3a-a01c-56e7515c0cb0" />
<br></br>

<img width="566" height="413" alt="image" src="https://github.com/user-attachments/assets/8fc31caf-480e-4b37-98b9-19586dbacb07" />
<br></br>


