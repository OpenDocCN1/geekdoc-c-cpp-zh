
```csharp
using System.Runtime.Serialization;

namespace IsolatedStorageDemo
{
    public static class IsoStoreHelper
    {
        public static void WriteGraphToFile<T>(string filename,
            T sourceObject)
        {
            using (IsolatedStorageFile isf =
                IsolatedStorageFile.GetUserStoreForApplication())
            {
                using (IsolatedStorageFileStream stream =
                    new IsolatedStorageFileStream(filename,
                        FileMode.Create, isf))
                {
                    DataContractSerializer dcs =
                        new DataContractSerializer(typeof(T));
                    dcs.WriteObject(stream, sourceObject);
                    stream.Close();
                }
            }
        }

        public static T ReadGraphFromFile<T>(string filename)
            where T:class
        {
            T result = null;
            using (IsolatedStorageFile isf =
                IsolatedStorageFile.GetUserStoreForApplication())
            {
                using (IsolatedStorageFileStream stream =
                    new IsolatedStorageFileStream(filename,
                        FileMode.OpenOrCreate, isf))
                {
                    if (stream.Length > 0)
                    {
                        DataContractSerializer dcs =
                            new DataContractSerializer(typeof(T));
                        result = dcs.ReadObject(stream) as T;
                    }
                }
            }
            return result;
        }
    }
}
```

```csharp
using System.Runtime.Serialization;

namespace IsolatedStorageDemo.Models
{
    [DataContract]
    public class Customer
    {
        [DataMember]
        public string Name { get; set; }
        [DataMember]
        public string Description { get; set; }
    }
}
```

The AppData and customer classes are used only as a means of storing and retrieving data. What the user interacts with is a view model, shown in Listing 14.4. The view model may contain data that looks like our data contract classes, but it also contains very UI-specific features, such as a property called IsSelected that we'll use to change the back-ground color of items in a list box. This view model is actually borrowed (okay, borderline hacked) from the view model that comes with the Databound Windows Phone Application Visual Studio template.

## Listing 14.4 MainViewModel.cs and ItemViewModel.cs

```
using System;
using System.ComponentModel;
using System.Collections.Generic;
using System.Collections.ObjectModel;
using IsolatedStorageDemo.Models;

namespace IsolatedStorageDemo
{
    public class MainViewModel
    {
        public MainViewModel()
        {
            this.Items = new ObservableCollection<ItemViewModel>();
        }

        public ObservableCollection<ItemViewModel> Items
        {
            get; private set;
        }

        public bool IsDataLoaded
        {
            get; private set;
        }
    }

    public class ItemViewModel : INotifyPropertyChanged
    {
        public ItemViewModel()
        {
            this.IsSelected = false;
        }

        public bool IsSelected { get; set; }

        public event PropertyChangedEventHandler PropertyChanged;

        public void OnPropertyChanged(string propertyName)
        {
            if (PropertyChanged != null)
            {
                PropertyChanged(this, new PropertyChangedEventArgs(propertyName));
            }
        }
    }
}
```

## Chapter 14 Local Storage on the Phone

```
get;
private set;
}
public void LoadData()
{
	LoadFromIso();
	this.IsDataLoaded = true;
}
public void LoadFromIso()
{
	AppData appData =
	IsoStoreHelper.ReadGraphFromFile<AppData>(
	"appdata.dat", () =>
	{
		AppData seed = new AppData()
		{
			Customers = new Customer[] {
				new Customer { Name = "First Customer",
					Description = "This is the first customer" } }
		};
		return seed;
	});
	this.Items.Clear();
	foreach (Customer cust in appData.Customers)
	{
		this.Items.Add(new ItemViewModel { Name = cust.Name,
			Description = cust.Description });
	}
}
public void SaveToIso()
{
	AppData data = new AppData();
	List<Customer> customerList = new List<Customer>();
	foreach (ItemViewModel itemView in this.Items)
	{
		customerList.Add(new Customer { Name = itemView.Name,
			Description = itemView.Description });
	}
	data.Customers = customerList.ToArray();
	IsoStoreHelper.WriteGraphToFile("appdata.dat", data);
}
```

```
}

using System;
using System.ComponentModel;

namespace IsolatedStorageDemo
{
    public class ItemViewModel : INotifyPropertyChanged
    {
        private string _name;
        public string Name
        {
            get
            {
                return _name;
            }
            set
            {
                if (value != _name)
                {
                    _name = value;
                    NotifyPropertyChanged("Name");
                }
            }
        }

        private string _description;
        public string Description
        {
            get
            {
                return _description;
            }
            set
            {
                if (value != _description)
                {
                    _description = value;
                    NotifyPropertyChanged("Description");
                }
            }
        }

        private bool _isSelected;
        public bool IsSelected
        {
```

```
get
{
    return _isSelected;
}
set
{
    _isSelected = value;
    NotifyPropertyChanged("IsSelected");
}
}

public event PropertyChangedEventHandler PropertyChanged;
private void NotifyPropertyChanged(String propertyName)
{
    PropertyChangedEventHandler handler = PropertyChanged;
    if (null != handler)
    {
        handler(this, new PropertyChangedEventArgs(propertyName));
    }
}
}
```

Now that we’ve got a data model that we can load from and write to isolated storage, and we have a view model that is tailored for Silverlight data binding, the only thing we’re missing is a UI to put it all together. Listing 14.5 contains the XAML for rigging up the list box to display the customers in our view model. In addition, it contains an application bar with buttons we can use to add and remove customers. Each time a customer is added or removed, we convert the view model into a data model and save it to isolated storage. When the application starts up, the view model tries to reconstitute itself from saved data in isolated storage.

## Listing 14.5 MainPage.xaml

```
<phone:PhoneApplicationPage
    x:Class="IsolatedStorageDemo.MainPage"

    ...namespace stuff removed for clarity ...
    d:DataContext="{d:DesignData SampleData/MainViewModelSampleData.xaml}"
    FontFamily="{StaticResource PhoneFontFamilyNormal}"
    FontSize="{StaticResource PhoneFontSizeNormal}"
    Foreground="{StaticResource PhoneForegroundBrush}"
    SupportedOrientations="Portrait" Orientation="Portrait"
    xmlns:my="clr-namespace:IsolatedStorageDemo.Converters"
    shell:SystemTray.IsVisible="True">
<phone:PhoneApplicationPage.Resources>
```

```
<my:SelectedColorConverter x:Key="colorConverter"/>
</phone:PhoneApplicationPage.Resources>

<Grid x:Name="LayoutRoot" Background="Transparent">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>

    <StackPanel x:Name="TitlePanel" Grid.Row="0" Margin="12,17,0,28">
        <TextBlock x:Name="ApplicationTitle"
                   Text="Iso Store App"
                   Style="{StaticResource PhoneTextNormalStyle}"/>
        <TextBlock x:Name="PageTitle"
                   Text="Customers" Margin="9,-7,0,0"
                   Style="{StaticResource PhoneTextTitle1Style}"/>
    </StackPanel>

    <Grid x:Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
        <ListBox x:Name="MainListBox" Margin="0,0,-12,0"
                 ItemsSource="{Binding Items}"
                 SelectionChanged="MainListBox_SelectionChanged">
            <ListBox.ItemTemplate>
                <DataTemplate>
                    <StackPanel Margin="0,0,0,17" Width="432"
                                Background="{Binding Path=IsSelected,
                                          Converter={StaticResource colorConverter}}">
                        <TextBlock Text="{Binding Name}"
                                   TextWrapping="Wrap"
                                   Style="{StaticResource PhoneTextExtraLargeStyle}"/>
                        <TextBlock Text="{Binding Description}"
                                   TextWrapping="Wrap" Margin="12,-6,12,0"
                                   Style="{StaticResource PhoneTextSubtleStyle}"/>
                    </StackPanel>
                </DataTemplate>
            </ListBox.ItemTemplate>
        </ListBox>
    </Grid>
</Grid>

<phone:PhoneApplicationPage.ApplicationBar>
    <shell:ApplicationBar IsVisible="True" IsMenuEnabled="false">
        <shell:ApplicationBarIconButton x:Name="appBarAddButton"
                                        IconUri="/Images/appbar.add.rest.png"
                                        Text="Add" Click="appBarAddButton_Click"/>
    </shell:ApplicationBar>
</phone:PhoneApplicationPage.ApplicationBar>
```
