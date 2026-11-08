Let’s perform the following steps to understand the execution of LINQ to Entities by using the LINQ project:

+   1. Modify the relational database schema of the project by adding some more tables in the schema. In our case, we have added two more tables:
+   Product and Department. The schema structure of the two tables is given as follows:

```
```
Product {Product_ID, Product_Name, Dept_ID}
Department {Dept_ID, Dept_Name}
```
```

+   2. Modify the Employee table of the relational database schema to include Product_ID as a foreign key in the table. Therefore, the new schema structure of the Employee table will be as follows:

```
```
Employee {Employee_ID, First_Name, Last_Name, Designation, Product_ID*}
```
```

+   3. Select File → View → Solution Explorer in Visual Studio 2008. The Solution Explorer pane appears. Right-click the LINQ project from the pane. A context menu appears.

+   4. Select the Add option from the context menu. A sub-context menu appears.

+   5. Select the New Item option from the sub-context menu.
+   The Add New Item - LINQ dialog box appears.

+   6. Add a new ADO.NET Entity Data Model in the project and name it as LINQ.edmx, as shown in Figure 19.14:

![](bbox=[0.216, 0.455, 0.809, 0.682])

Figure 19.14: Adding a New ADO.NET Entity Data Model

+   7. Click the Add button. The Entity Data Model Wizard appears (Figure 19.15).

+   8. Select the model content from the wizard. In our case, we have selected Generate from database, as shown in Figure 19.15: