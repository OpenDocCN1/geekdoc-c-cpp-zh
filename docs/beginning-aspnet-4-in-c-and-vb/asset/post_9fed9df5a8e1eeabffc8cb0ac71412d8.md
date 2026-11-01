
## MultiTrigger

A property trigger fires when a value of a property changes. If you need to set a trigger because two or more properties have a specific value, you can use MultiTrigger.

MultiTrigger has a Conditions property where valid values of properties can be specified. It also has a Setters property, where the properties that need to be set can be specified. In the example, a style is defined for TextBox elements where the trigger applies if the IsEnabled property is True and the Text property has the value Test. If both apply, the Foreground property of the TextBox is set to Red:

```xml
<Window x:Class="TriggerDemo.MultiTriggerWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MultiTriggerWindow" Height="300" Width="300">
    <Window.Resources>
        <Style TargetType="TextBox">
            <Style.Triggers>
                <MultiTrigger>
                    <MultiTrigger.Conditions>
                        <Condition Property="IsEnabled" Value="True" />
                        <Condition Property="Text" Value="Test" />
                    </MultiTrigger.Conditions>
                    <MultiTrigger.Setters>
                        <Setter Property="Foreground" Value="Red" />
                    </MultiTrigger.Setters>
                </MultiTrigger>
            </Style.Triggers>
        </Style>
    </Window.Resources>
    <Grid>
        <TextBox />
    </Grid>
</Window>
```

*code snippet TriggerDemo/MultiTriggerWindow.xaml*

## Data Triggers

Data triggers fire if bound data to a control fulfills specific conditions. In the following example, a Book class is used that has different displays depending on the publisher of the book.

The Book class defines the properties Title and Publisher and has an overload of the ToString() method:

```csharp
public class Book
{
    public string Title { get; set; }
    public string Publisher { get; set; }

    public override string ToString()
    {
        return Title;
    }
}
```

*code snippet TriggerDemo/Book.cs*

In the XAML code, a style is defined for ListBoxItem elements. The style contains DataTrigger elements that are bound to the Publisher property of the class that is used with the items. If the value of the Publisher property is Wrox Press, the Background is set to Red. With the publishers Dummies and Sybex, the Background is set to Yellow and LightBlue accordingly:

```xml
<Window x:Class="TriggerDemo.DataTriggerWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="Data Trigger Window" Height="300" Width="300">
<Window.Resources>
<Style TargetType="ListBoxItem">
<Style.Triggers>
<DataTrigger Binding="{Binding Path=Publisher}" Value="Wrox Press">
<Setter Property="Background" Value="Red" />
</DataTrigger>
<DataTrigger Binding="{Binding Path=Publisher}" Value="Dummies">
<Setter Property="Background" Value="Yellow" />
</DataTrigger>
<DataTrigger Binding="{Binding Path=Publisher}" Value="Sybex">
<Setter Property="Background" Value="LightBlue" />
</DataTrigger>
</Style.Triggers>
</Style>
</Window.Resources>
<Grid>
<ListBox x:Name="list1" />
</Grid>
</Window>
```

code snippet TriggerDemo/DataTriggerWindow.xaml

In the code-behind, the list with the name list1 is initialized to contain several Book objects:

```csharp
public DataTriggerWindow()
{
InitializeComponent();
list1.Items.Add(new Book
{
Title = "Professional C# 4.0",
Publisher = "Wrox Press"
});
list1.Items.Add(new Book
{
Title = "C# 2008 for Dummies",
Publisher = "Dummies"
});
list1.Items.Add(new Book
{
Title = "Mastering Integrated HTML and CSS",
Publisher = "Sybex"
});
}
```

code snippet TriggerDemo/DataTriggerWindow.xaml.cs

Running the application, you can see in Figure 35-21 the ListBoxItem elements that are formatted according to the publisher value.

With DataTrigger, multiple properties must be set for MultiDataTrigger (similar to Trigger and MultiTrigger).

![](img/d7d2ffa0a76feaab821930e95daace93_1072_0.png)

## TEMPLATES

In this chapter, you have already seen that a Button control can have any content. The content can be simple text, but you can also add a Canvas element, which can contain shapes. You can add a Grid, or a video to the button. However, there is even more than that you can do with a button!

```xml
<Ellipse.Fill>
    <LinearGradientBrush StartPoint="0,0" EndPoint="0,1">
        <GradientStop Offset="0" Color="#aaffffff" />
        <GradientStop Offset="1" Color="Transparent" />
    </LinearGradientBrush>
</Ellipse.Fill>
<ContentPresenter Name="GelButtonContent"
    VerticalAlignment="Center"
    HorizontalAlignment="Center"
    Content="{TemplateBinding Content}" />
</Grid>
</ControlTemplate>
</Setter.Value>
```

code snippet TemplateDemo/StyledButtonWindow.xaml

Such a styled button now looks very fancy on the screen. There's still a problem: there is no action if the mouse is clicked or the mouse moves over the button. This isn't the typical feeling a user has with a button. This can be solved: with a template-styled button, you must have triggers for the button to appear differently in response to mouse moves and mouse clicks.

![](img/d7d2ffa0a76feaab821930e95daace93_1075_0.png)

FIGURE 35-23

Using property triggers (discussed previously), this can be solved easily. The triggers just need to be added to the Triggers collection of the ControlTemplate as shown. Here, two triggers are defined. One property trigger is active when the IsMouseOver property of the button is true. Then the Fill property of the ellipse with the name GelBackground is changed to a RadialGradientBrush with values from Lime to DarkGreen. With the IsPressed property, other colors are specified for the RadialGradientBrush:

```xml
<ControlTemplate.Triggers>
    <Trigger Property="IsMouseOver" Value="True">
        <Setter Property="Ellipse.Fill" TargetName="GelBackground">
            <Setter.Value>
                <RadialGradientBrush>
                    <GradientStop Offset="0" Color="Lime" />
                    <GradientStop Offset="1" Color="DarkGreen" />
                </RadialGradientBrush>
            </Setter.Value>
        </Setter>
    </Trigger>
    <Trigger Property="IsPressed" Value="True">
        <Setter Property="Ellipse.Fill" TargetName="GelBackground">
            <Setter.Value>
                <RadialGradientBrush>
                    <GradientStop Offset="0" Color="#ffcc34" />
                    <GradientStop Offset="1" Color="#cc9900" />
                </RadialGradientBrush>
            </Setter.Value>
        </Setter>
    </Trigger>
</ControlTemplate.Triggers>
```

Now you can run the application and see a visual feedback from the button as soon as the mouse hovers over it or the mouse is clicked.

## Data Templates

The content of ContentControl elements can be any content — not only WPF elements but also .NET objects. For example, an object of the Country type can be assigned to the content of a Button class. The Country class has been created to represent the name and flag with a path to an image. This class defines the Name and ImagePath properties, and it has an overridden ToString() method for a default string representation:

```csharp
public class Country
{
    public string Name { get; set; }
    public string ImagePath { get; set; }

    public override string ToString()
    {
        return Name;
    }
}
```

code snippet TemplateDemo/Country.cs

How does this content look within a Button or any other ContentControl? By default, the ToString() method is invoked, and the string representation of the object is shown. For a custom look you can also create a DataTemplate for the Country type.

Here, within the resources of the Window, a DataTemplate is created. This DataTemplate doesn't have a key assigned and thus is a default for the Country src type — it is also the alias of the XML namespace referencing the .NET assembly and .NET namespace. Within the DataTemplate the main elements are a TextBox with the Text property bound to the Name property of the Country, and an Image with the Source property bound to the ImagePath property of the Country. The Grid, Border, and Rectangle elements define the layout and visual appearance:

```xml
<Window.Resources>
    <DataTemplate DataType="{x:Type src:Country}">
        <Grid>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="Auto" />
                <ColumnDefinition Width="Auto" />
            </Grid.ColumnDefinitions>
            <Grid.RowDefinitions>
                <RowDefinition Height="50" />
            </Grid.RowDefinitions>
            <TextBlock FontSize="16" VerticalAlignment="Center" Margin="5"
                Text="{Binding Name}" FontWeight="Bold" Grid.Column="0" />
            <Border Margin="4,0" Grid.Column="1" BorderThickness="2"
                CornerRadius="4">
                <Border.BorderBrush>
                    <LinearGradientBrush StartPoint="0,0" EndPoint="0,1">
                        <GradientStop Offset="0" Color="#aaa" />
                        <GradientStop Offset="1" Color="#222" />
                    </LinearGradientBrush>
                </Border.BorderBrush>
                <Grid>
                    <Rectangle>
                        <Rectangle.Fill>
                            <LinearGradientBrush StartPoint="0,0" EndPoint="0,1">
                                <GradientStop Offset="0" Color="#444" />
                                <GradientStop Offset="1" Color="#fff" />
                            </LinearGradientBrush>
                        </Rectangle.Fill>
                    </Rectangle>
                    <Image Width="48" Margin="2,2,2,1"
                        Source="{Binding ImagePath}" />
                </Grid>
            </Border>
        </Grid>
    </DataTemplate>
</Window.Resources>
```

code snippet TemplateDemo/StyledButtonWindow.xaml
