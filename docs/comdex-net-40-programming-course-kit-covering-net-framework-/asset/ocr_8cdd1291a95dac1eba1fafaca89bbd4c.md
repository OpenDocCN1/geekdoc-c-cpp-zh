+   11. Select the desired table from the drop-down list. In our case, we have selected the **Employees** table (Fig.C#-5.19).
+   12. *Set* the **Size** property of the **DataGridView** control to **643, 262**.
+   13. *Drag and drop* a **SqlDataAdapter** control to the **Form2** form and *configure* it to the **Employees** table.
+   14. *Double-click* the **Form2** form at design time and *add* the code, given in Listing 5.8, in its **Load** event:

# Listing 5.8: Adding Data to a Dataset

```
```csharp
private void Form2_Load(object sender, EventArgs e)
{
    sqlDataAdapter1.Fill(dataSet1, "Employees");
}
```
```

In Listing 5.8, the **Fill()** method is used to fill the dataset (**dataSet1**) with data from the **Employees** table.

+   15. *Set* the **Form2** form as the **Startup** form in the **Program.cs** file.

> > **You have already learned how to set a form as the startup form in chapter 2, Windows Forms, in Visual Basic 2010 section.**

+   16. *Press* the **F5** key to execute the application. The output appears, as shown in Fig.C#-5.20:

![](bbox=[0.334, 0.379, 0.688, 0.506])

Fig.C#-5.20

In addition to binding a control using the **DataSource** and **DataMember** properties at design time, you can also bind the **DataGridView** control at runtime, as shown in the following code snippet:

```
```csharp
dataGridView1.DataSource = dataSet1;
dataGridView1.DataMember = "Employees";
```
```

In the preceding code snippet, the first line sets the **DataSource** property of the **dataGridView1** data grid view to the **dataSet1** dataset. The second line sets the **DataMember** property to the **Employees** table.

After learning about the different processes of data binding in Windows Form applications, let’s now learn how to implement data binding in WPF applications.

# Data Binding in WPF

WPF allows you to design a robust and visually appealing user interface. You can accomplish data binding with WPF controls similar to the Windows controls. In WPF, you can implement data binding using the code-behind file of an application, Extensible Application Markup Language (XAML), or a combination of both.

Similar to other applications, such as the Windows Forms and the ASP.NET Web applications, WPF also needs to have a target and a source for data binding. Generally the target is a control and the source is some data. The target of the binding can be a property of the control, for example, the **Text** property of the **TextBox** control. You can select the property of the control in WPF to bind your data, which includes properties of other controls, or any data source such as the **northwind** database. In short, you can say that data binding is one of the most powerful features included in WPF.

> > **You have already learned about WPF in chapter 5, Windows Presentation Foundation, of Visual Basic 2010 section.**