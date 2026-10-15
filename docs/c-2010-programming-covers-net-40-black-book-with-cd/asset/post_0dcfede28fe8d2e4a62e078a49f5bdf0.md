
```
mc:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="500">
<Grid x:Name="LayoutRoot" Background="White">
    <Border BorderThickness="4" BorderBrush="DarkBlue">
        <StackPanel Background="Beige">
            <TextBlock Margin="7" FontSize="18" FontFamily="Comic Sans MS" FontWeight="Bold" Foreground="DeepPink">
                Displaying the use of an AutoCompleteBox Control</TextBlock>
            <StackPanel x:Name="Layout" Orientation="Horizontal">
                <StackPanel.Resources>
                    <Style x:Key="myTBStyle" TargetType="TextBox">
                        <Setter Property="Background" Value="LightYellow" />
                        <Setter Property="Foreground" Value="DarkSlateGray" />
                        <Setter Property="Margin" Value="5" />
                        <Setter Property="FontWeight" Value="Bold" />
                        <Setter Property="FontSize" Value="14" />
                        <Setter Property="BorderBrush" Value="DarkGray" />
                    </Style>
                    <Style x:Key="myLBStyle" TargetType="ListBoxItem">
                        <Setter Property="Background" Value="khaki" />
                        <Setter Property="Foreground" Value="DarkSlateGray" />
                        <Setter Property="Margin" Value="5" />
                        <Setter Property="FontStyle" Value="Italic" />
                        <Setter Property="FontSize" Value="14" />
                        <Setter Property="BorderBrush" Value="DarkGray" />
                    </Style>
                </StackPanel.Resources>
                <TextBox Height="30" Width="Auto" IsReadOnly="True" Text="Enter a City Name:" Style="{StaticResource myTBStyle}" BorderBrush="LightGray" />
                <my:AutoCompleteBox Width="300" x:Name="myACB" TextBoxStyle="{StaticResource myTBStyle}" ItemContainerStyle="{StaticResource myLBStyle}" IsTextCompletionEnabled="True" MinimumPopulateDelay="0" MinimumPrefixLength="1"/>
            </StackPanel>
        </StackPanel>
    </Border>
</Grid>
</UserControl>
```

In Listing 17.14, you can see that an AutoCompleteBox control, myACB, is used whose appearance has been changed by creating new styles. A Style tag with a unique key value, myTBStyle, is used to declare a style as a static resource and assign value for the TextBoxStyle property of the text box in the AutoCompleteBox control, myACB. Similarly, a style with a unique key value, myLBStyle, is declared as a static resource and set as value for the ItemContainerStyle property of the drop-down list in the AutoCompleteBox control, myACB. An AutoCompleteBox control, myACB, which uses the style defined for its text box and drop-down list is then used. Note that the IsTextCompletion property of the AutoCompleteBox control, myACB, is set to true to enable the auto-completion of the text as you type some text into the text box. In addition, the MinimumPopulateDelay and MinimumPrefixLength properties of the AutoCompleteBox control, myACB, are also set to 0 and 1, respectively.

- 2. Open the code-behind file of the MyAutoCompleteBoxCS application and type the code, as shown in Listing 17.15:

## Listing 17.15: Showing the Code for the Code-Behind File of the MainPage.xaml File of the MyAutoCompleteBoxCS Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;
namespace MyAutoCompleteBoxCS {
    public partial class MainPage : UserControl {
        public MainPage() {
            InitializeComponent();
            List<string> cityNames=new List<string>();
            cityNames.Add("Arizona");
            cityNames.Add("Atlanta");
            cityNames.Add("California");
            cityNames.Add("Chicago");
            cityNames.Add("Colorado");
            cityNames.Add("Denver");
            cityNames.Add("Detroit");
            cityNames.Add("Durham");
            cityNames.Add("Florida");
            cityNames.Add("Georgia");
            cityNames.Add("Hamilton");
            cityNames.Add("Hampshire");
            cityNames.Add("Lancaster");
            cityNames.Add("Las Vegas");
            cityNames.Add("Los Angeles");
            cityNames.Add("Michigan");
            cityNames.Add("New Jersey");
            cityNames.Add("New Orleans");
            cityNames.Add("New York");
            cityNames.Add("North Carolina");
            cityNames.Add("Ohio");
            cityNames.Add("Olympia");
            cityNames.Add("San Diego");
            cityNames.Add("San Francisco");
            cityNames.Add("San Jose");
            cityNames.Add("Seattle");
            cityNames.Add("Washington");
            cityNames.Add("Texas");
            myACB.ItemsSource = cityNames;
        }
    }
}
```

- 3. Run the MyAutoCompleteBoxCS application. The output appears, as shown in Figure 17.42:

![](img/e073a4882197be4ab61103cbe0bcb394_931_0.png)

Figure 17.42: Displaying the Output of the MyAutoCompleteBoxCS Application

With this, you have learned how to use an AutoCompleteBox control in your Silverlight applications. Next, let’s see how the DataPager control can be used in the Silverlight applications.

## Using the DataPager Control

As you know, that Silverlight DataPager is a control that represents the UI to provide paging capabilities to other controls, such as DataGrid and ListBox. In other words, it means that using a DataPager control, you can include paging behavior to other Silverlight controls. Now, perform the following steps to use the DataPager control to page through the data in a DataGrid control in a Silverlight application:

- 1. Create a Silverlight application named SilverlightDataPagerCS (available on the CD). Listing 17.16 shows the code for the MainPage.xaml file of the SilverlightDataPagerCS Silverlight application:

## Listing 17.16: Showing the Code for the MainPage.xaml File of the SilverlightDataPagerCS Application

```
<UserControl xmlns:my="clr-namespace:System.Windows.Controls.Data"
x:Class="SilverlightDataPagerCS.MainPage"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="400">
<Grid x:Name="LayoutRoot" Background="Black" Height="300" Width="400">
<StackPanel x:Name="ContentStackPanel" Orientation="Vertical">
<my:DataGrid x:Name="myDatagrid" Height="200" Width="400"/>
<my:DataPager x:Name="myPager" Source="{Binding Path=ItemsSource, ElementName=myDatagrid}" DisplayMode="Numeric"/>
</StackPanel>
</Grid>
</UserControl>
```

In the preceding listing, a DataGrid and a DataPager control, myDatagrid and myPager, respectively are used. The DataPager control, myPager, is used to display the data items inside the DataGrid control, myDatagrid, in multiple pages.

- 2. Open the code-behind file of the MainPage.xaml file of the SilverlightDataPagerCS application and type the code, as shown in Listing 17.17:

## Listing 17.17: Showing the Code for the Code-Behind File of the MainPage.xaml File of the SilverlightDataPagerCS Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;
using System.Windows.Data;
namespace SilverlightDataPagerCS {
public partial class MainPage : UserControl {
public MainPage() {
InitializeComponent();
PagedCollectionView pagedcollectionview = new PagedCollectionView("W E L C O M E T O S I L V E R L I G H T 3".Split(' '));
pagedcollectionview.PageSize = 5;
myDatagrid.ItemsSource = pagedcollectionview;
}
}
```
