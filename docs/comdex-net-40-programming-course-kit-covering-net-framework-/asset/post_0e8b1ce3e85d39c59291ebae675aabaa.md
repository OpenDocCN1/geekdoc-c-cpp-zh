
In this application, it is assumed that a data connection with the Northwind database is established and data adapter and dataset objects are created.

- 9. Drag and drop a **ComboBox** control from the **Toolbox** to the **Form1** form at design time.
- 10. Select the **ComboBox** control and in the **Properties** window, click the drop-down arrow beside the **DataSource** property. A drop-down list appears (Fig.C#-5.7).
- 11. *Expand* the **Other Data Sources** node in the drop-down list (Fig.C#-5.7).
- 12. *Expand* the **Form1 List Instances** node. A list of data sources appears (Fig.C#-5.7).
- 13. *Select* the dataset named **DataSet1** (Fig.C#-5.8).

![](img/9862a98a1a2d3bb14334137965a1ec60_388_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_388_1.png)

Fig.C#-5.7

Fig.C#-5.8

- 14. *Select* the **DisplayMember** property and click the drop-down arrow beside it. A drop-down list appears (Fig.C#-5.9).
- 15. *Expand* the **Employees** table to display all the fields (Fig.C#-5.9).
- 16. *Select* **FirstName** from the list of fields in the **Employees** table (Fig.C#-5.10).

![](img/9862a98a1a2d3bb14334137965a1ec60_388_2.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_388_3.png)

Fig.C#-5.9

Fig.C#-5.10

Setting the **DisplayMember** property to the **FirstName** field of the **Employees** table displays the first name of all the employees in a combo box.

- 17. *Select* the **ValueMember** property and *click* the drop-down arrow beside it. A drop-down list appears (Fig.C#-5.9).
- 18. *Expand* the **Employees** table to display all the fields (Fig.C#-5.11).
- 19. *Select* **EmployeeID** from the list of fields in **Employees** table (Fig.C#-5.12).

![](img/9862a98a1a2d3bb14334137965a1ec60_389_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_389_1.png)

Setting the **ValueMember** property to **EmployeeID** field of the **Employees** table displays the employee IDs using the **SelectedValue** property of the **ComboBox** control.

- 20. *Double-click* the **Form1** form and add the code, given in Listing 5.6, in its **Load** event:

### Listing 5.6: Showing the Code to Add Data to a Dataset

```csharp
private void Form1_Load(object sender, EventArgs e)
{
    sqlDataAdapter1.Fill(dataSet11, "Employees");
}
```

In Listing 5.6, the **Fill()** method is used to fill the dataset (**dataSet11**) with data from the **Employees** table.

- 21. *Double-click* the **ComboBox** control at design time and add the code, given in Listing 5.7, in the **SelectedIndexChanged** event:

### Listing 5.7: Showing the Code to Access the Employee ID

```csharp
private void comboBox1_SelectedIndexChanged(object sender, EventArgs e)
{
    MessageBox.Show(comboBox1.SelectedValue.ToString(), "Employee ID",
        MessageBoxButtons.OK);
}
```

In Listing 5.7, when you select the employee name from the combo box, the employee ID of the selected employee is displayed in a message box.

- 22. Press the **F5** key to execute the application. You can see the combo box displaying the values from the field (**FirstName**) you specified for the **DisplayMember** property (Fig.C#-5.13).
- 23. *Select* an employee’s first name from the combo box. A message box appears, displaying the corresponding value from the field (**EmployeeID**) you specified for the **ValueMember** property (Fig.C#-5.14).

![](img/9862a98a1a2d3bb14334137965a1ec60_389_2.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_389_3.png)

In addition to binding a **ComboBox** control using the **DataSource**, **DisplayMember**, and **ValueMember** properties at design time, you can bind the **ComboBox** control at runtime, as shown in the following code snippet:

```csharp
comboBox1.DataSource= dataSet11;
comboBox1.DisplayMember= "Employees.FirstName";
comboBox1.ValueMember = "Employees.EmployeeID";
```

In the preceding code snippet, the **DataSource** property of a combo box named **comboBox1** is set to a dataset named **dataSet11**. The **DisplayMember** property of the combo box is set to the **FirstName** field and the **ValueMember** property is set to the **EmployeeID** field of the **Employees** table.

Let’s now learn about the DataMember property.

## The DataMember Property

The **DataMember** property is supported by the **DataGridView** control, which can display an entire table from a dataset. You can enable data binding in a **DataGridView** control by using two properties, **DataSource** and **DataMember**. The **DataSource** property represents the data source for the binding, which is typically a dataset and the **DataMember** property represents the name of the table to be displayed in a **DataGridView** control. In the **ComplexDataBinding** application, let’s perform the following steps to bind a **DataGridView** control with the **Employees** table of the **dataSet11** dataset:

- 1. *Right-click* the **ComplexDataBinding** application in **Solution Explorer** and select **Add → Windows Form** from the context menu to add a new form to the application, as shown in Fig.C#-5.15:

![](img/9862a98a1a2d3bb14334137965a1ec60_390_0.png)

Fig.C#-5.15

The Add New Item dialog box appears, as shown in Fig.C#-5.16:

![](img/9862a98a1a2d3bb14334137965a1ec60_390_1.png)

Fig.C#-5.16

- 2. Click the **Add** button to add the **Form2** form to the application (Fig.C#-5.16).
- 3. *Set* the **Text** property of the **Form2** to **Using the DataMember Property**.
- 4. *Set* the **Size** property of the **Form2** form to **662, 300**.
- 5. *Drag and drop* a **DataGridView** control from the **Data** tab of the **Toolbox** to the **Form2** form. A Smart Tag automatically appears, as shown in Fig.C#-5.17:

![](img/9862a98a1a2d3bb14334137965a1ec60_391_0.png)

Fig.C#-5.17

- 6. Click the drop-down arrow beside the **Choose Data Source** option. A drop-down list appears, as shown in Fig.C#-5.18:

![](img/9862a98a1a2d3bb14334137965a1ec60_391_1.png)

Fig.C#-5.18

- 7. *Expand* the **Other Data Sources** node in the drop-down list (Fig.C#-5.18).
- 8. *Expand* the **Project Data Sources** node. A list of data sources appears (Fig.C#-5.18).
- 9. *Select* the dataset named **DataSet1** (Fig.C#-5.18).
- 10. Select the **DataMember** property and *click* the drop-down arrow beside it in the **Properties** window. A drop-down list appears, as shown in Fig.C#-5.19.

![](img/9862a98a1a2d3bb14334137965a1ec60_391_2.png)

Fig.C#-5.19

- 11. Select the desired table from the drop-down list. In our case, we have selected the **Employees** table (Fig.C#-5.19).
- 12. *Set* the **Size** property of the **DataGridView** control to **643, 262**.
- 13. *Drag and drop* a **SqlDataAdapter** control to the **Form2** form and *configure* it to the **Employees** table.
- 14. *Double-click* the **Form2** form at design time and *add* the code, given in Listing 5.8, in its **Load** event:

### Listing 5.8: Adding Data to a Dataset

```csharp
private void Form2_Load(object sender, EventArgs e)
{
    sqlDataAdapter1.Fill(dataSet1, "Employees");
}
```

In Listing 5.8, the **Fill()** method is used to fill the dataset (**dataSet1**) with data from the **Employees** table.

- 15. *Set* the **Form2** form as the **Startup** form in the **Program.cs** file.

> **You have already learned how to set a form as the startup form in chapter 2, Windows Forms, in Visual Basic 2010 section.**

- 16. *Press* the **F5** key to execute the application. The output appears, as shown in Fig.C#-5.20:

![](img/9862a98a1a2d3bb14334137965a1ec60_392_0.png)

Fig.C#-5.20

In addition to binding a control using the **DataSource** and **DataMember** properties at design time, you can also bind the **DataGridView** control at runtime, as shown in the following code snippet:

```csharp
dataGridView1.DataSource = dataSet1;
dataGridView1.DataMember = "Employees";
```

In the preceding code snippet, the first line sets the **DataSource** property of the **dataGridView1** data grid view to the **dataSet1** dataset. The second line sets the **DataMember** property to the **Employees** table.

After learning about the different processes of data binding in Windows Forms applications, let’s now learn how to implement data binding in WPF applications.

## Data Binding in WPF

WPF allows you to design a robust and visually appealing user interface. You can accomplish data binding with WPF controls similar to the Windows controls. In WPF, you can implement data binding using the code-behind file of an application, Extensible Application Markup Language (XAML), or a combination of both.

Similar to other applications, such as the Windows Forms and the ASP.NET Web applications, WPF also needs to have a target and a source for data binding. Generally the target is a control and the source is some data. The target of the binding can be a property of the control, for example, the **Text** property of the **TextBox** control. You can select the property of the control in WPF to bind your data, which includes properties of other controls, or any data source such as the **Northwind** database. In short, you can say that data binding is one of the most powerful features included in WPF.

> **You have already learned about WPF in chapter 5, Windows Presentation Foundation, of Visual Basic 2010 section.**
