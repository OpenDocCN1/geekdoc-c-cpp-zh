# Using DataGrids

Data Grids are used to display data from a table in a grid like format. When a user see’s table data, they normally prefer seeing all the table rows in one shot. This can be achieved if we can display the data in a grid on the form.

C# and Visual Studio have inbuilt data grids, this can be used to display data. Let’s take a look at an example of this. In our example, we will have a data grid, which will be used to display the Tutorial ID and Tutorial Name values from the demotb table.

**Step 1)** Drag the DataGridView control from the toolbox to the Form in Visual Studio. The DataGridView control is used in Visual Studio to display the rows of a table in a grid-like format.

![](bbox=[0.05, 0.44, 0.92, 0.68])

**Step 2)** In the next step, we need to connect our data grid to the database. In the last section, we had created a project data source. Let’s use the same data source in our example.

+   1. First, you need to choose the grid and click on the arrow in the grid. This will bring up the grid configuration options.
+   2. In the configuration options, just choose the data source as demotbBindingSource which was the data source created in the earlier section.