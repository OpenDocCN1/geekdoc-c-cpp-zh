
4. Change the window properties like this:
```
Title="Options" Height="345" Width="434" ResizeMode="NoResize"
```
5. Delete the StackPanel and all of its content.
6. Delete the Canvas control with the Grid.Row property set to 3 and all of its content.
7. Delete the Label control from the Canvas control with the Grid.Row property set to 1.
8. Change the Label control in the Canvas with the Grid.Row property set to 0 like this:
```
<Label Canvas.Right="10" Canvas.Top="13" Content="Options" Foreground="#FFF7EFFF" FontFamily="Times New Roman" FontSize="24" FontWeight="Bold" />
```
9. Drag a StackPanel into the bottom row and set its properties to this:
```
Grid.Row="3" Orientation="Horizontal" FlowDirection="RightToLeft"
```
10. Add two buttons to the StackPanel like this:
```
<Button Content="_Cancel" Height="22" Width="75" Margin="10,0,0,0" Name="cancelButton" />
<Button Content="_OK" Height="22" Width="75" Margin="10,0,0,0" Name="okButton" />
```
11. Drag a TabControl into the second row and set its properties like this:
```
Grid.RowSpan="2" Canvas.Left="10" Canvas.Top="2" Width="408" Height="208"
Grid.Row="1"
```
12. Change the Header property of each of the two TabItem controls to Game and Computer Player, respectively.

Your window now looks like Figure 14-11 and it is time to insert some content into the tab items.

![](img/cf72ea860016d2d680fc085fc06f265a_471_0.png)

FIGURE 14-11

13. Select the Game TabItem and drag a CheckBox control onto it. Set its properties like this:
```
Content="Play against computer" HorizontalAlignment="Left" Margin="11,33,0,0" VerticalAlignment="Top" Name="playAgainstComputerCheck"
```
14. Drag a Label control and then a ComboBox control into the TabItem and set their properties like this:
```
<Label Content="Number of players" HorizontalAlignment="Left" Margin="10,54,0,0" VerticalAlignment="Top" />
<ComboBox HorizontalAlignment="Left" Margin="196,58,0,0" VerticalAlignment="Top" Width="86" Name="numberOfPlayersComboBox" SelectedIndex="0">
<ComboBoxItem>2</ComboBoxItem>
<ComboBoxItem>3</ComboBoxItem>
<ComboBoxItem>4</ComboBoxItem>
</ComboBox>
```
15. Select the second TabItem with the header Computer Player. Drag a Label and three RadioButtons onto the Grid and set their properties like this:
```
<Label Content="Skill Level" HorizontalAlignment="Left" Margin="10,10,0,0" VerticalAlignment="Top"/>
<RadioButton Content="Dumb" HorizontalAlignment="Left" Margin="37,41,0,0" VerticalAlignment="Top" IsChecked="True" Name="dumbAIRadioButton"/>
<RadioButton Content="Good" HorizontalAlignment="Left" Margin="37,62,0,0" VerticalAlignment="Top" Name="goodAIRadioButton"/>
<RadioButton Content="Cheats" HorizontalAlignment="Left" Margin="37,83,0,0" VerticalAlignment="Top" Name="cheatingAIRadioButton"/>
```
16. The layout of the window is now complete. Open the App.xaml file and change StartupUri to Options.xaml.

17. Run the application.

## How It Works

The window's ResizeMode is set to NoResize. You can therefore position the controls without regard to what happens if the window changes size, because the user can no longer resize the window.

The StackPanel in Step 9 has a new property, FlowDirection, which is set to RightToLeft. This causes the two buttons that are added to it to cling to the right edge of the dialog box rather than the left edge that is the default. Interestingly, this also changes the meaning of the Margin property of the two buttons, causing Left and Right to be swapped.

The RadioButtons on the second tab are set up without specifying a GroupName, which causes them to be grouped together. You set the IsChecked property to true on the first one, which makes this the default selection.

```
{
    private GameOptions _gameOptions;
    public Options()
    {
        if (_gameOptions == null)
        {
            if (File.Exists("GameOptions.xml"))
            {
                using (var stream = File.OpenRead("GameOptions.xml"))
                {
                    var serializer = new XmlSerializer(typeof(GameOptions));
                    _gameOptions = serializer.Deserialize(stream) as GameOptions;
                }
            }
            else
                _gameOptions = new GameOptions();
        }
        InitializeComponent();
    }
}
```

5. Go to Design View and double-click each of the three RadioButtons to add the Checked event handler to the code-behind file. Change the handlers like this:
```
private void dumbAIRadioButton_Checked(object sender, RoutedEventArgs e)
{
    _gameOptions.ComputerSkill = ComputerSkillLevel.Dumb;
}
private void goodAIRadioButton_Checked(object sender, RoutedEventArgs e)
{
    _gameOptions.ComputerSkill = ComputerSkillLevel.Good;
}
private void cheatingAIRadioButton_Checked(object sender, RoutedEventArgs e)
{
    _gameOptions.ComputerSkill = ComputerSkillLevel.Cheats;
}
```
6. Return to Design View and select the TextBox on the Game tab. Click the lightning icon on the Properties panel and double-click the GotFocus event to add the handler to the code-behind file.

7. Enter this code:
```
private void timeAllowedTextBox_GotFocus(object sender, RoutedEventArgs e)
{
    timeAllowedTextBox.SelectAll();
}
```
8. Select the TextBox again in Design View and add the PreviewMouseLeftButtonDown event handler to the code-behind file.

9. Enter this code:
```
private void timeAllowedTextBox_PreviewMouseLeftButtonDown(object sender,
    MouseButtonEventArgs e)
{
    var control = sender as TextBox;
    if (control == null)
        return;
    Keyboard.Focus(control);
    e.Handled = true;
}
```
10. Run the application.

## How It Works

The new class is currently just a number of properties that store the values from the Options window. It is marked as `Serializable` to make it possible to save it to a file.

The `Checked` event of a `RadioButton` is raised whenever the user selects it. You handle this event in order to set the value of the `ComputerSkillLevel` property of the `GameOptions` instance.

## Data Binding

Data binding is a way of declaratively connecting controls with data. In the Options window, you handled the `Checked` event of the `RadioButtons` in order to set the value of the `ComputerSkillLevel` property in the `GameOptions` class. This works well, and you can use code and event handling to set all the values you have in a window, but very often it is better to bind the properties of your controls directly to the data.

A binding consists of four components:

- The binding target, which specifies the object on which the binding is used
- The target property, which specifies the property to set
- The binding source, which specifies the object used by the binding
- The source property, which specifies which property holds the data

You don't always set all of these elements explicitly; particularly the binding target is very often implicitly specified by the fact that you are setting a binding to a property on a control.

The binding source is always set in order to make a binding work, but it can be set in several ways. In the following sections and in Chapter 15, you are going to see several ways of binding data from sources.

## The DataContext

A `DataContext` control defines a data source that can be used for data binding on all child elements of an element. You will often have a single instance of a class that holds most of the data that is used in a view. If this is the case you can set the `DataContext` of the window to the instance of that object, which makes you able to bind properties from that class in your view. This is demonstrated in the “Dynamic Binding to External Objects” section.

```csharp
public class NumberOfPlayers : ObservableCollection<int>
{
    public NumberOfPlayers()
    : base()
    {
        Add(2);
        Add(3);
        Add(4);
    }
}
```

3. Return to the Options.xaml file's Design View and select the Window root element.

4. Select the Canvas element that contains the ComboBox and add this code below it, and above the TabControl declaration.

```xml
<Canvas.Resources>
    <local:NumberOfPlayers x:Key="numberOfPlayersData" />
</Canvas.Resources>
```

5. Select the ComboBox and remove the three ComboBoxItems from it.

6. Add this property to it:
```
ItemsSource="{Binding Source={StaticResource numberOfPlayersData}}"
```

## How It Works

There is a lot happening in this example. The class NumberOfPlayers derives from a special collection named ObservableCollection. This base class is a collection that has been extended to make it work better with WPF. In the constructor of the class, you add the values to the collection.

Next you create a new resource on the Canvas. You could have created this resource on any parent element of the ComboBox. When a resource is specified on an element, all child elements can use it.

Finally you set the ItemsSource to a binding. The ItemsSource property is specifically designed to allow you to specify a binding for the collection of items on an Items control. In the binding you just need to specify the binding source. The binding target, target property, and source property settings are handled by the ItemsSource property.

## Dynamic Binding to External Objects

Now you can bind to objects that are created on the fly as they are needed in order to provide some data. What if you already have an instantiated object that you want to use for data binding? In that case, you need to do a little plumbing in the code.

In the case of the Options window, you don't want the options to be cleared every time the window is opened, and you want the selections the user made to persist and be used in the rest of the application.

You can do this in code by setting the value of the DataContext property to the instance.
