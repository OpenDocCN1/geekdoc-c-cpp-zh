
```csharp
params string[] names
{
    this.name = name;
    this.age = age;
    this.profile = profile;
    this.id = id;
    foreach (string Employee in names)
    {
        this.names.Add(Employee);
    }
}
public Data()
: this("", "", "", "")
{
}
private string name;
public string Name
{
    get { return name; }
    set { name = value; }
}
private string age;
public string Age
{
    get { return age; }
    set { age = value; }
}
private string profile;
public string Profile
{
    get { return profile; }
    set { profile = value; }
}
private string id;
public string EmployeeID
{
    get { return id; }
    set { id = value; }
}
public override string ToString()
{
    return name;
}
private readonly List<string> names = new List<string>();
public string[] Names
{
    get { return names.ToArray(); }
}
}
```

In Listing 8.11, a class named Data is created. The class Data contains five data members, which are name, age, profile, id, and names. Using properties, values have been assigned to the data members of the Data class.

- 8. Add the highlighted code given in Listing 8.12 to the MainWindow.xaml.cs file:

### Listing 8.12: Showing the Code to add in the MainWindow.xaml.cs File

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
namespace BindingToCLRObject
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        private Data name1 = new Data();
        public MainWindow()
        {
            InitializeComponent();
            nameGrid.DataContext = name1;
        }
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            string message = name1.EmployeeID;
            string caption = name1.Name;
            MessageBox.Show(message, caption);
        }
    }
}
```

- 9. Press the F5 key to execute the **BindingtoCLRObject** application. The output appears, as shown in Fig.C8-35.

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_292_0.png)

**Fig.C8-35**

In Fig.C8-35, you can see that the **Binding to a CLR Object** window appears in which you can enter employee details.

- 10. Enter the employee details in the text boxes (Fig.C8-36).

- 11. Click the **Show Data** button. A message box appears (Fig.C8-36).

- 12. Click the **OK** button in the message box to close it, as shown in Fig.C8-36.

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_292_1.png)

**Fig.C8-36**

As shown in Fig.C8-36, when you click the **Show Data** button, a message box appears. The title of the message box is bound to the name of the employee you entered in the **Binding to a CLR Object** window, and it displays the ID of the employee.

In this section, you learned how to perform binding to CLR objects, such as properties of controls. Now, let's learn to perform binding to ADO.NET objects.

## Binding to ADO.NET Objects

You can also bind an ADO.NET object to a WPF application. For example, you can bind a data table to a WPF application. You can implement the **IBindingList** interface to provide change notifications. The **IBindingList** interface provides features that support both complex and simple data binding to a data source. While binding your WPF application to an ADO.NET object, the first step is to create a connection with a database. After establishing the connection, the adapter is created, which executes the SQL statement to retrieve the record from the database. The result is stored in the data table of the dataset by calling the **Fill()** method of the adapter. This result is then displayed in the WPF control.

To bind a WPF application to an ADO.NET object, you first need to create a connection string to bind your WPF application to an ADO.NET object. You then need to bind your controls by specifying the **ItemsSource** and **ItemTemplate** properties. To display a particular column data, you should specify the **DisplayMemberBinding** property. Let's create an application in which you can bind an ADO.NET object to a WPF application. For this, perform the following steps:

- 1. Create a WPF application named **BindingtoADO.NET**.
- 2. Set the title of the **MainWindow** window to **Binding to ADO.NET** by using the **Title** property.
- 3. Add the highlighted code given in Listing 8.13 to the **MainWindow.xaml** file.

### Listing 8.13: Adding the Code in the MainWindow.xaml File

```xml
<Window x:Class="BindingtoADO.NET.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Binding to ADO.NET" Height="300" Width="500">
    <Grid x:Name="Grid1">
        <ListView Name="ListViewEmployeeDetails" Margin="0,0,0,53"
            ItemTemplate="{DynamicResource EmployeeTemplate}" ItemsSource="{Binding Path=Table}">
            <ListView.Background>
                <LinearGradientBrush>
                    <GradientStop Color="Bisque" Offset="0"/>
                    <GradientStop Color="DarkOrange" Offset="1"/>
                </LinearGradientBrush>
            </ListView.Background>
            <ListView.View>
                <GridView>
                    <GridViewColumn Header="Employee ID"
                        DisplayMemberBinding="{Binding Path=EmployeeID}"/>
                    <GridViewColumn Header="First Name" DisplayMemberBinding="{Binding Path=FirstName}"/>
                    <GridViewColumn Header="Last Name" DisplayMemberBinding="{Binding Path=LastName}"/>
                    <GridViewColumn Header="City" DisplayMemberBinding="{Binding Path=City}"/>
                    <GridViewColumn Header="Country" DisplayMemberBinding="{Binding Path=Country}"/>
                </GridView>
            </ListView.View>
        </ListView>
        <Button Height="40" Margin="162,0,163,0" Name="button1"
            VerticalAlignment="Bottom">Click Me</Button>
        <Label Height="28" HorizontalAlignment="Left" Margin="11,10,0,0" Name="label1"
            VerticalAlignment="Top" Width="142" FontSize="13">Data from SQL Server</Label>
    </Grid>
</Window>
```

With the help of the code given in Listing 8.13, you can prepare the interface on which you can display your data.

- 4. Import two namespaces, System.Data and System.Data.SqlClient, in the code-behind file of the Binding to ADO.NET application, as shown in the following code-snippet:

```csharp
using System.Data;
using System.Data.SqlClient;
```

- 5. Add the highlighted code given in Listing 8.14 to the MainWindow.xaml.cs file:

### Listing 8.14: Showing the Code to Add in the MainWindow.xaml.cs File

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
using System.Data;
using System.Data.SqlClient;
namespace BindingtoADO.NET
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }
        private void button1_Click(object sender, RoutedEventArgs e)
        {
            SqlConnection mycon = new SqlConnection();
            SqlDataAdapter myadapter = new SqlDataAdapter();
            SqlCommand cmd = new SqlCommand();
            String dataquery = "SELECT EmployeeID, FirstName, LastName, City, Country FROM Employees";
            cmd.CommandText = dataquery;
            myadapter.SelectCommand = cmd;
            mycon.ConnectionString = "Data Source=TEMP-PC\SQLEXPRESS;Initial Catalog=D:\\SQL SAMPLE DATABASE\NORTHWND.MDF;Integrated Security=True";
            cmd.Connection = mycon;
            DataSet ds = new DataSet();
            myadapter.Fill(ds);
            ListViewEmployeeDetails.DataContext = ds.Tables[0].DefaultView;
            mycon.Close();
        }
    }
}
```

In Listing 8.14, we bind the WPF application to the Employees table of the NORTHWND database by using the DataContext object.

- 6. Press the F5 key to execute the BindingtoADO.NET application. The output appears, as shown in Fig.C8-37:
