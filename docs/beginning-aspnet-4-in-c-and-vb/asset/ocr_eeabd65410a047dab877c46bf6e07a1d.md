```
```xml
d:DesignHeight="300" d:DesignWidth="300">
    <Grid>
        <TreeView ItemsSource="{Binding}">
            <TreeView.Resources>
                <HierarchicalDataTemplate DataType="{x:Type local:Championship}" ItemsSource="{Binding Races.Value}">
                    <TextBlock Text="{Binding Year}" />
                </HierarchicalDataTemplate>

                <HierarchicalDataTemplate DataType="{x:Type local:F1Race}" ItemsSource="{Binding Results.Value}">
                    <StackPanel Orientation="Horizontal">
                        <TextBlock Text="{Binding Country}" Margin="5,0,5,0" />
                        <TextBlock Text="{Binding Path=Date, StringFormat=d }" Margin="5,0,5,0" />
                    </StackPanel>
                </HierarchicalDataTemplate>

                <DataTemplate DataType="{x:Type local:F1RaceResult}">
                    <StackPanel Orientation="Horizontal">
                        <TextBlock Text="{Binding Position}" Margin="5,0,5,0" />
                        <TextBlock Text="{Binding Racer}" Margin="5,0,0,0" />
                        <TextBlock Text=", " />
                        <TextBlock Text="{Binding Car}" />
                    </StackPanel>
                </DataTemplate>
            </TreeView.Resources>
        </TreeView>
    </Grid>
</UserControl>
```
```

code snippet Formula1Demo/TreeUC.xaml

Now for the code that fills the hierarchical control. In the code-behind file of the XAML code, DataContext is assigned to the Years property. The Years property uses a LINQ query, instead of the ADO.NET Entity Framework data context, to get all the years of the Formula-1 races in the database and to create a new Championship object for every year. With the instance of the Championship class, the Year property is set. This class also has a Races property to return the races of the year; however, this information is not yet filled in.

![](bbox=[0.12, 0.66, 0.88, 0.74])

```
```csharp
using System.Collections.Generic;
using System.Linq;
using System.Windows.Controls;

namespace Formula1Demo
{
    public partial class TreeUC : UserControl
    {
        private Formula1Entities data = new Formula1Entities();

        public TreeUC()
        {
            InitializeComponent();
            this.DataContext = Years;
        }
    }
```
```