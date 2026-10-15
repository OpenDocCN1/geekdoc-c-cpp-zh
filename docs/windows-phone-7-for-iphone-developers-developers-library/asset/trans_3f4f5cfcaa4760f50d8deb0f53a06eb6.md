

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

AppData 和 Customer 类仅用作存储和检索数据的手段。用户与之交互的是视图模型，如清单 14.4 所示。视图模型可能包含看起来与我们的数据协定类相似的数据，但它也包含非常特定于 UI 的功能，例如一个名为 IsSelected 的属性，我们将使用它来更改列表框中项的背景颜色。这个视图模型实际上是从 Visual Studio 的“Databound Windows Phone Application（数据绑定 Windows Phone 应用程序）”模板附带的视图模型中借用（好吧，勉强算是拼凑）而来的。

## 清单 14.4 MainViewModel.cs 和 ItemViewModel.cs

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

## 第14章 手机上的本地存储

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

现在我们有了一个可从独立存储加载并写入的数据模型，也有了专为 Silverlight 数据绑定定制的视图模型，唯一缺失的就是一个将这些整合在一起的 UI。清单 14.5 包含了用于搭建列表框以显示视图模型中客户的 XAML。此外，它还包含一个带有按钮的应用程序栏，我们可以用它来添加和删除客户。每次添加或删除客户时，我们都会将视图模型转换为数据模型，并将其保存到独立存储中。当应用程序启动时，视图模型会尝试从独立存储中已保存的数据重新构建自身。

## 清单 14.5 MainPage.xaml

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

