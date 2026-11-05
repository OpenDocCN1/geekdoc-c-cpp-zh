![](bbox=[0.175, 0.096, 0.237, 0.145])

Two additional controls on the navigational tool strip are shown in Figure 14-33. The **Retrieve By Last Name** button uses the value entered in the text box to its left to populate the data grid.

# Displaying Data Using Details View

Instead of displaying data in a gridlike structure, a **Details** view is also available. When you select **Details** and drag the entire table onto the form, you get Label and TextBox objects for each column in the dataset, as shown in Figure 14-34.

![](bbox=[0.176, 0.29, 0.791, 0.613])

Figure 14-34  Details view

When you drag the full dataset table over to the form, you get a preset label identifying the text box’s value. The label is the column identifier with spaces replacing underscores. Of course, if you select the label object, you can change its Text property from the Properties window. You do not have to drag the full set of columns; you can pick and choose from the Data Sources window and selectively drag the columns of interest.

When you are displaying data from multiple tables, you will need to change the SelectCommand for the TableAdapter so that data from both tables can be retrieved. After adding the Data Source, recall that the DataSet Designer Tool is accessed by double clicking on the dataSet icon in the Solution Explorer Window. For the ConfigToolsExample, the SelectCommand CommandText property for the StudentTableAdapter was modified using the Query Builder Tool. A second table, Department, was added to the diagram pane. The tables were automatically linked, which enabled the matching data from both tables to be retrieved. Before testing the