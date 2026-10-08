# Export Data to a DataSet

A great feature of DataManipulator is that it can export chart data to a DataSet object. You can use this for saving chart data, or passing it to other controls that work with DataSet.

The DataManipulatorSample application demonstrates this feature by passing the exported DataSet to a form that displays a DataGridView object. The following code implements this task:

```
private void ExportDataToDataSetMenuItem_Click(object sender, EventArgs e)
{
    var dataSet = chart1.DataManipulator.ExportSeriesValues();
    var exportForm = new ExportedDataForm(dataSet);
    exportForm.ShowDialog();
}
```

The essential work is done by the ExportSeriesValues method that produces a DataSet instance holding all data. Each series is put in a separate table within the data set. ExportedDataForm class has its data in its constructor and sets up the ExportedDataGrid object:

```
public partial class ExportedDataForm : Form
{
    public ExportedDataForm()
    {
        InitializeComponent();
    }

    public ExportedDataForm(DataSet dataSet) : this()
    {
        ExportedDataGrid.DataSource = dataSet;
        ExportedDataGrid.DataMember = "Series1";
    }
}
```

The ExportedDataGrid object can display only one data at a time. The code sets it through the DataMember property to Series1.

# Apply Statistical Formula to Data

Through the Statistics property of the DataManipulator class, you can access statistical operations such as mean, covariance, correlation calculations, and many more. The following code snippet shows how to calculate and display the correlation between Series1 and Series2:

```
private void ApplyStatisticsMenuItem_Click(object sender, EventArgs e)
{
    var corrValue = chart1.DataManipulator.Statistics.
    Correlation("Series1", "Series2");
    MessageBox.Show(String.Format("Correlation between the series is: {0}",
    corrValue));
}
```