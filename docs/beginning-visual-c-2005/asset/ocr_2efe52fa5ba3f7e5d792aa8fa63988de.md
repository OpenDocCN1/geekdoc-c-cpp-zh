# Accessing Data Sources in a Windows Forms Application

![](bbox=[0.12, 0.13, 0.88, 0.53])

Figure 22-17

You can see that three objects have been added to the project as a result of adding the data source: the NorthWindDataSet object that encapsulates the database, the CustomersTableAdapter object that accesses the data in the Customers table in the database, and the CustomersBindingSource object that manages the communications between the database and the DataGridView control.

The application is now complete, and so far you have not written a single line of code. That's quite remarkable considering the amount of function you have in the program; however, when I ran the program, the column headers look a little cramped. I prefer the column widths to be set to accommodate the text in the rows, so I couldn't resist adding the following two lines of code to the Form1 class constructor:

```
dataGridView->AutoSizeColumnsMode = DataGridViewAutoSizeColumnsMode::AllCells;
dataGridView->AutoResizeColumnHeaders();
```

The application window now looks as shown in Figure 22-18.