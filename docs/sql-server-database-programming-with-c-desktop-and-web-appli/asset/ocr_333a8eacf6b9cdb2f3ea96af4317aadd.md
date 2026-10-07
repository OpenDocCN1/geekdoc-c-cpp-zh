# 202

# SQL Server Database Programming with C#

DataGrid Form

| faculty_id | faculty_name | title | office | phone | college | email | fimage |
|---|---|---|---|---|---|---|-|
| A25956 | Black Anderson | Professor | MTC-218 | 750-378-9987 | Virginia Tech | banderson@colle... | |
| A77588 | Debbie Angles | Associate Professor | MTC-320 | 750-330-2276 | University of Chica... | dangle@colle... | |
| B66750 | Alice Brown | Assistant Professor | MTC-257 | 750-230-6550 | University of Florida | brown@colle... | |
| B78880 | Ying Bai | Associate | MTC-211 | 750-378-1148 | Florida Atlantic Uni... | ybai@colle... | |
| B66590 | Davya Hall | Associate Professor | MTC-224 | 750-238-1061 | University of Notre... | dhalla@colle... | |
| J1201110 | Henry Henry | | MTC-350 | 750-329-6050 | Ohio State Univers... | jhenry@colle.e... | |
| J33486 | Steve Johnson | Distinguished Professor | MTC-118 | 750-320-1146 | Harvard University | sjohnson@colle... | |
| K56980 | Jenny King | Professor | MTC-324 | 750-320-1216 | East Florida Univer... | jking@colle... | |

FIGURE 5.34 The entire view for the faculty table.

Using this grid tool, you can not view data from the faculty table, but also add new and delete data from the table by clicking the ( Add (+) ) or Delete (x) button to do that. Just add a new line in your table by clicking the Add you want to add data, or delete the data you want to delete by clicking the browsing arrow on the top of the window and then clicking the Delete button. You need to know that these modifications can only affect your data in the DataSet, it has nothing to do with data in your real database.

When you drag the Faculty table from the source window to the DataGridForm, what happened during this? Let's take a little more look at this issue. To do that, click the Close button to stop your project's running.

First, from the first view of the graphical interface, as we mentioned, five instances of design tools are created and have been added to this project, Second, from some view of the project codes, instructions have been automatically added into this project, Open the code window by right-clicking on it in the Solution Explorer window and clicking the View Code item from the popup menu. Browse to the method DataGrid_Load() and you can find that line of instruction in here is:

```
this.facultyTableAdapter.Fill(this.CSE_DeptDataSet.Faculty);
```

The functionality of this instruction is that the Fill() method, which belongs to the TableTableAdapter class, is to load data from the faculty table into the database in the DataSet, and furthermore into your DataGridView view. The Fill is a very powerful method and it performs an equivalent operation to that of a SQL SELECT statement. To make this clearer, open the Data Source window and right-click on any place inside that. Select the Edit DataSet to open the DataSet Designer Wizard. Right-click on the bottom line, in which the Fill() and the GetData() methods are shown, on the faculty table, and select the Configure item to open the TableAdapter Configuration Wizard. You will find that a complete SQL statement is already stated in here:

SELECT faculty_id, faculty_name, title, office, college, phone,
Email, fimage FROM dbo.Faculty

This statement will be executed when the Fill() method is called by the facultyTable-Adapter as the DataGrid_Load() event runs when you start this project. The data returned from executing this statement will fill the grid view in the Faculty Form.