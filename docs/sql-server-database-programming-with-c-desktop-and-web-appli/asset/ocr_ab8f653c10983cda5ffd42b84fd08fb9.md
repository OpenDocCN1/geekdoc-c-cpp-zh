# Data Selection Query with Visual C#.NET

BindingSource component. All further interactions with the data, including navigating, sorting, filtering, and updating, are accomplished with calls to the BindingSource component.

Second, the BindingSource component can act as a strongly typed data source. Adding a type to the BindingSource component with the Add method creates a list of that type.

Third, the BindingSource control works as a bridge to connect the data to controls on your Visual C# forms with your data (DataSet). The BindingSource can also be considered as a container object and all mapped data from that source. As a data-driven process runs, the BindingSource will be filled with data from the DataSet using a TableAdapter. In addition, the BindingSource control will create a set of data that is mapped to filled data in the DataSet. The BindingSource can hold this set of mapped data and create a one-to-one connection between the DataSet and the BindingSource. This connection is very useful when you perform data binding between your controls on the Visual C# form and the data in the DataSet. In fact, you set up a connection when data is needed to be reflected on the associated controls, a request to BindingSource and the BindingSource control will control the access to the data source (DataSet) and data updating in those controls. For instance, the DataGridView will send a request to the BindingSource control when a column sorting action is performed, and the latter will communicate with the data source to complete this sorting.

When perform a data binding in Visual Studio, you need to bind the data referenced by the BindingSource control to property of your controls.

# 5.1.1.4 BindingNavigator

The BindingNavigator allows users to select and browse all records stored in the data source (DataSet) by one in a sequence. The BindingNavigator component provides a standard UI with buttons and enables users to navigate to the first and the previous records as well as the next and last records in the data. It also provides textboxes to display how many records existed in the current data table and the current record's index.

As shown in Figure 5.2, the BindingNavigator is also bound to the BindingSource component. When the user clicks either the Previous or the Next button on the BindingNavigator UI, a request is sent to the BindingSource for the previous or the next record, in this turn, request is sent to the data source for picking up that data.

# 5.1.1.5 TableAdapter

From Figure 5.2, one can find that a TableAdapter is equivalent to an adapter and it just works as a connection method between the database and DataSet, and between the BindingSource and the DataSet. This means that the TableAdapter has dual functionalities when it works as different roles for the different purposes. For example, as you develop your data-driven applications using the DataSet using the TableAdapter's Fill method. The TableAdapter also works as an adapter to coordinate the data operations between the BindingSource and the DataSet when the data controls in Visual C# form needs to be filled or updated.

Prior to Visual Studio 2005, the Data Adapter was the only link between the DataSet and the database. If a change is needed in the data, you need to use a different TableAdapter for each table in the DataSet and to call the Update method of each Data Adapter.

The TableAdapter is introduced in Visual Studio 2005 and you cannot find this from the Tool Window. The TableAdapter belongs to designer-generated component that connect your DataSet Objects with their underlying databases, and it will be automatically created when you add and configure data sources such as DataSet Configuration Wizard.

The TableAdapter is similar to Adapter in that both components can handle the data operations between DataSet and database, but the TableAdapter can contain multiple queries to support multiple tables from the database, allowing one TableAdapter to perform multiple queries to