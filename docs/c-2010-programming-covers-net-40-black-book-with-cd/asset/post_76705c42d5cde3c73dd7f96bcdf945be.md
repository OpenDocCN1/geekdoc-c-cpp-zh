
**Listing 10.23: Showing the Code for Extending an Existing Style**

```xml
<Window x:Class="ExtendingStyle.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MainWindow" Height="350" Width="525">
    <Window.Resources>
        <Style x:Key="BigFontButtonStyle">
            <Setter Property="Control.FontFamily" Value="Times New Roman" />
            <Setter Property="Control.FontSize" Value="18" />
            <Setter Property="Control.FontWeight" Value="Bold" />
        </Style>
        <Style x:Key="EmphasizedBigFontButtonStyle"
               BasedOn="{StaticResource BigFontButtonStyle}">
            <Setter Property="Control.Foreground" Value="White" />
            <Setter Property="Control.Background" Value="DarkBlue" />
        </Style>
    </Window.Resources>
    <Grid>
        <Button Height="41" Margin="26,24,39,0" Name="button1" VerticalAlignment="Top"
                Style="{StaticResource BigFontButtonStyle}">Using BigFontStyle</Button>
        <Button Height="35" Margin="26,94,39,0" Name="button2"
                VerticalAlignment="Top">Normal Button</Button>
        <Button Margin="0,0,0,69" Name="button3" Height="39" VerticalAlignment="Bottom"
                Style="{StaticResource EmphasizedBigFontButtonStyle}">Using EmphasizedBigFontButtonStyle</Button>
    </Grid>
</Window>
```

In Listing 10.23, there are three Button controls added to the window. The first Button control has the style applied by the first style (BigFontButtonStyle). The BigFontButtonStyle style defines three font properties. The second Button control is a normal control with no style applied to it. The third Button control has the style applied by the second style (EmphasizedBigFontButtonStyle), which extends the first style, BigFontButtonStyle, and adds two more properties for changing the foreground and the background of the Button control. You can extend an existing style by using the BasedOn property. You can run the application by pressing the F5 key.

Figure 10.55 shows the output of Listing 10.23:

![](img/e073a4882197be4ab61103cbe0bcb394_482_0.png)

## Using DataTemplate to Change the Appearance of the Content of Control

In WPF, you can use the DataTemplate template to change the appearance of the data type of a control. This is done by using the DataType property of the DataTemplate template. This property gets or sets the type for which you need to use the DataTemplate template in the application. For example, there might be a case where you want one template to display both the Boolean value and String value. The DataType property is helpful in such scenarios. Let’s use the DataType property to change the appearance of the data type of a control. Create a WPF application named UsingDataTemplate_ChangeAppearance (available in the CD) and add the code to the MainWindow.xaml file, as shown in Listing 10.24:

**Listing 10.24: Showing the Code to Use DataTemplate**

```xml
<Page
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:sys="clr-namespace:System;assembly=mscorlib">
    <Page.Resources>
        <DataTemplate DataType="{x:Type sys:Boolean}">
            <CheckBox IsChecked="{Binding Mode=OneWay}" />
        </DataTemplate>
    </Page.Resources>
    <ItemsControl Width="100" Height="100">
        <sys:Int32>30</sys:Int32>
        <sys:DateTime>12/16/1970</sys:DateTime>
        <sys:Boolean>False</sys:Boolean>
        <sys:Boolean>True</sys:Boolean>
        <sys:String>Hello</sys:String>
        <sys:Boolean>True</sys:Boolean>
    </ItemsControl>
</Page>
```

In Listing 10.24, each Boolean value is displayed as a CheckBox control, rather than as a True or False value. This is done using the DataType property of DataTemplate.

After adding the code to the MainWindow.xaml file, add the code in Listing 10.25 to the MainWindow.xaml.cs file:

**Listing 10.25: Adding Code to the MainWindow.xaml.cs File**

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
namespace UsingDataTemplate_ChangeAppearance
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            throw new NotImplementedException();
        }
    }
}
```

You can run the application by pressing the F5 key. The output is shown in Figure 10.56:

![](img/e073a4882197be4ab61103cbe0bcb394_484_0.png)

**Figure 10.56: Changing the Appearance of a Control**

## Using ControlTemplate

The ControlTemplate template specifies the structure of a control that can be shared across multiple instances of the control. Let’s use the ControlTemplate in a WPF application. Create a WPF application named UsingControlTemplate (available in the CD) and add the following code to the MainWindow.xaml file, as shown in Listing 10.26:

**Listing 10.26: Showing the Code for Implementing ControlTemplate**

```xml
<Window x:Class="UsingControlTemplate.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MainWindow" Height="350" Width="525">
    <Window.Resources>
        <Style x:Key="ButtonStyle" TargetType="{x:Type Button}">
            <Setter Property="Template">
                <Setter.Value>
                    <ControlTemplate>
                        <Grid>
                            <Grid.RowDefinitions>
                                <RowDefinition Height="2*"/>
                                <RowDefinition Height="*"/>
                            </Grid.RowDefinitions>
                            <Rectangle RadiusX="4" RadiusY="8" Margin="2">
                                <Rectangle.Fill>
                                    <LinearGradientBrush StartPoint="0,0" EndPoint="0,1">
                                        <GradientStop Offset="0" Color="LightBlue"/>
                                        <GradientStop Offset="0.5" Color="Gold"/>
                                        <GradientStop Offset="1" Color="PaleGreen"/>
                                    </LinearGradientBrush>
                                </Rectangle.Fill>
                            </Rectangle>
                        </Grid>
                    </ControlTemplate>
                </Setter.Value>
            </Setter>
        </Style>
    </Window.Resources>
    <StackPanel>
        <Button Name="Button1" Height="41" />
        <Button Name="Button2" Height="41" />
        <Button Name="Button3" Style="{StaticResource ButtonStyle}" Height="71">TemplateButton</Button>
    </StackPanel>
</Window>
```

Listing 10.26 adds three Button controls to the window. No style is applied to the first two Button controls; whereas, the ControlTemplate template is applied to the third button. Run the application by pressing the F5 key.

Figure 10.57 shows the output of Listing 10.26:

![](img/e073a4882197be4ab61103cbe0bcb394_485_0.png)

**Figure 10.57: Using the Control Template**

## Using the DataTemplate Template

A DataTemplate template describes the visual structure of a data object. This template is particularly useful when you are binding an ItemsControl, such as a ListBox control, to an entire collection. Let’s use a DataTemplate template in a WPF application. Create a WPF application named UsingDataTemplate (available in the CD) and add the following code to the MainWindow.xaml file, as shown in Listing 10.27:

**Listing 10.27: Showing the Code for Implementing a DataTemplate Template**

```xml
<Window x:Class="UsingDataTemplate.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="350" Width="525">
    <Window.Resources>
        <XmlDataProvider x:Key="myTasks" XPath="Tasks/Task">
            <x:XData>
                <Tasks xmlns="">
                    <Task Name="Groceries"/>
                    <Task Name="Laundry"/>
                    <Task Name="Mail"/>
                </Tasks>
            </x:XData>
        </XmlDataProvider>
    </Window.Resources>
    <ListBox HorizontalContentAlignment="Stretch"
        ItemsSource="{Binding Source={StaticResource myTasks}}">
        <ListBox.ItemTemplate>
            <DataTemplate>
                <DataTemplate.Resources>
                    <Style TargetType="TextBlock">
                        <Setter Property="FontSize" Value="18"/>
                        <Setter Property="HorizontalAlignment" Value="Center"/>
                    </Style>
                </DataTemplate.Resources>
                <Grid>
                    <Ellipse Fill="silver"/>
                    <StackPanel>
                        <TextBlock Margin="3,3,3,0" Text="{Binding XPath=@Name}"/>
                        <TextBlock Margin="3,0,3,7" Text="{Binding XPath=@Priority}"/>
                    </StackPanel>
                </Grid>
            </DataTemplate>
        </ListBox.ItemTemplate>
        <ListBox.ItemContainerStyle>
```
