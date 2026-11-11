**('Value1', 1), --Here, I'm inserting Value1 into Column_Name1 and the number 1 in Column_Name2.**

+   - ('Value2', 2),
+   - ('Value3', 3)

Now, it is time to insert data into your Department table. Insert the values as shown below. For example, the Department Name of Marketing must have a Department ID of 1, and so on.

+   - Department_Id: 1, Department_Name: Marketing
+   - Department_Id: 2, Department_Name: Development
+   - Department_Id: 3, Department_Name: Sales
+   - Department_Id: 4, Department_Name: Human Resources
+   - Department_Id: 5, Department_Name: Customer Support
+   - Department_Id: 6, Department_Name: Project Management
+   - Department_Id: 7, Department_Name: Information Technology
+   - Department_Id: 8, Department_Name: Finance/Payroll
+   - Department_Id: 9, Department_Name: Research and Development

UPDATE - Allows you to update existing data. For instance, you may change an existing piece of data in a table to another value.

It’s recommended to use caution when updating values in a table. You could give all rows within one column the same value if you don’t specify a condition in the WHERE clause.

# **--Updating a value or set of values in one column of a table**

```
UPDATE Table_Name
SET
```

**Column_Name1 = 'New Value 1', --Specify what your new value should be here**

Column_Name2 = 'New Value 2'

```
WHERE
```

**Column_Name1 = 'Old Value' --Using the WHERE clause as a condition**

**--Updates all rows in the table with the same value for one specific column**