
<Button>Button</Button>
</StackPanel>
</Window>

Figure 34.5 shows the child controls of the StackPanel organized vertically.

![](img/3d365b72b289213a91ade7eb366b8f35_1303_0.png)

Figure 34.5

## WrapPanel

The WrapPanel positions the children from left to right, one after the other, as long as they fit on one line, and then it continues with the next line. The panel’s orientation can be horizontal or vertical (code file LayoutSamples/WrapPanelWindow.xaml):

```
<Window x:Class="LayoutSamples.WrapPanelWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/
        xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/
        winfx/2006/xaml"
        Title="WrapPanelWindow" Height="300" Width="300">
    <WrapPanel>
        <WrapPanel.Resources>
            <Style TargetType="Button">
                <Setter Property="Width" Value="100" />
                <Setter Property="Margin" Value="5" />
            </Style>
        </WrapPanel.Resources>
        <Button>Button</Button>
        <Button>Button</Button>
        <Button>Button</Button>
        <Button>Button</Button>
<Button>Button</Button>
<Button>Button</Button>
<Button>Button</Button>
<Button>Button</Button>
</WrapPanel>
</Window>
```

Figure 34.6 shows the output of the panel. If you resize the application, the buttons are rearranged accordingly to have just that many buttons as fit in a line.

![](img/3d365b72b289213a91ade7eb366b8f35_1304_0.png)

Figure 34.6

## Canvas

Canvas is a panel that enables you to explicitly position controls. Canvas defines the attached properties Left, Right, Top, and Bottom that can be used by the children for positioning within the panel (code file LayoutSamples/CanvasWindow.xaml):

```
<Canvas Background="LightBlue">
    <Label Canvas.Top="30" Canvas.Left="20">Enter here:</Label>
    <TextBox Canvas.Top="30" Canvas.Left="120" Width="100" />
    <Button Canvas.Top="70" Canvas.Left="130" Content="Click Me!" Padding="5" />
</Canvas>
```

Figure 34.7 shows the output of the Canvas panel with the positioned children Label, TextBox, and Button.

# Figure 34.7

> NOTE The Canvas control is best used for the layout of graphic elements, like Shape controls shown in Chapter 30.

## DockPanel

The DockPanel is very similar to the Windows Forms docking functionality. Here, you can specify the area in which child controls should be arranged. DockPanel defines the attached property Dock; you can set the property in the children of the controls using the values Left, Right, Top, and Bottom. Figure 34.8 shows the outcome of text blocks with borders that are arranged in the dock panel. For easier differentiation, different colors are specified for the various areas (code file LayoutSamples/DockPanelWindow.xaml):

```
<DockPanel>
    <Border Height="25" Background="AliceBlue" DockPanel.Dock="Top">
        <TextBlock>Menu</TextBlock>
    </Border>
    <Border Height="25" Background="Aqua" DockPanel.Dock="Top">
        <TextBlock>Ribbon</TextBlock>
    </Border>
    <Border Height="30" Background="LightSteelBlue"
DockPanel.Dock="Bottom">
    <TextBlock>Status</TextBlock>
</Border>
<Border Height="80" Background="Azure" DockPanel.Dock="Left">
    <TextBlock>Left Side</TextBlock>
</Border>
<Border Background="HotPink">
    <TextBlock>Remaining Part</TextBlock>
</Border>
</DockPanel>
```

![](img/3d365b72b289213a91ade7eb366b8f35_1306_0.png)

Figure 34.8

## Grid

Using the Grid, you can arrange your controls with rows and columns. For every column, you can specify a ColumnDefinition. For every row, you can specify a RowDefinition. The following example code lists two columns and three rows. With each column and row, you can specify the width or height. ColumnDefinition has a Width dependency property; RowDefinition has a Height dependency property. You can define the height and width in pixels, centimeters, inches, or points, or you can set it to Auto to base the size on the content. The grid also allows star sizing, which means the space for the rows and columns is calculated according to the available space and relative to other rows and columns. When providing the available space for a column, you can

set the Width property to *. To have the size doubled for another column, you specify 2*. The sample code, which defines two columns and three rows, doesn't define additional settings with the column and row definitions; the default is the star sizing.

The grid contains several Label and TextBox controls. Because the parent of these controls is a grid, you can set the attached properties Column, ColumnSpan, Row, and RowSpan (code file LayoutSamples/GridWindow.xaml):

```
<Grid ShowGridLines="True">
    <Grid.ColumnDefinitions>
        <ColumnDefinition />
        <ColumnDefinition />
    </Grid.ColumnDefinitions>
    <Grid.RowDefinitions>
        <RowDefinition />
        <RowDefinition />
        <RowDefinition />
    </Grid.RowDefinitions>
    <Label Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="0" VerticalAlignment="Center" HorizontalAlignment="Center" Content="Title" />
    <Label Grid.Column="0" Grid.Row="1" VerticalAlignment="Center" Content="Firstname:" Margin="10" />
    <TextBox Grid.Column="1" Grid.Row="1" Width="100" Height="30" />
    <Label Grid.Column="0" Grid.Row="2" VerticalAlignment="Center" Content="Lastname:" Margin="10" />
    <TextBox Grid.Column="1" Grid.Row="2" Width="100" Height="30" />
</Grid>
```

The outcome of arranging controls in a grid is shown in Figure 34.9. For easier viewing of the columns and rows, the property ShowGridLines is set to true.

![](img/3d365b72b289213a91ade7eb366b8f35_1308_0.png)

# Figure 34.9

> NOTE For a grid in which every cell is the same size, you can use the UniformGrid class.

## Triggers

In Chapter 30, you can read about using the Visual State Manager that you can use to dynamically change the look of controls. The Visual State Manager is supported by both WPF and the Universal Windows Platform. WPF also offers property triggers for the same scenario, and there are other trigger types for different scenarios. This section discusses property triggers, multi-triggers, and data triggers.

With triggers, you can change the look and feel of your controls dynamically based on certain events or property value changes. For example, when the user moves the mouse over a button, the button can change its look. Usually, you need to do this with the C# code. With WPF, you can also do this with XAML as long as only the UI is influenced.

Property triggers are activated as soon as a property value changes. Multi-triggers are based on multiple property values. Event triggers fire

> NOTE If the IsPressed property is set to true, the IsMouseOver property will be true as well. Pressing the button also requires the mouse to be over the button. Pressing the button triggers it to fire and changes the properties accordingly. Here, the order of triggers is important. If the IsPressed property trigger is moved before the IsMouseOver property trigger, the IsMouseOver property trigger overwrites the values that the first trigger set.

You don’t need to reset the property values to the original values when the reason for the trigger is not valid anymore. For example, you don’t need to define a trigger for IsMouseOver=true and IsMouseOver=false. As soon as the reason for the trigger is no longer valid, the changes made by the trigger action are reset to the original values automatically.

Figure 34.10 shows the trigger sample application in which the foreground and font size of the button are changed from their original values when the button has the focus.

![](img/3d365b72b289213a91ade7eb366b8f35_1310_0.png)

> **NOTE** When using property triggers, it is extremely easy to change the look of controls, fonts, colors, opacity, and the like. When the mouse moves over them, the keyboard sets the focus—not a single line of programming code is required.

The `Trigger` class defines the following properties to specify the trigger action.

| Trigger Property | Description |
|---|---|
| `PropertyValue` | With property triggers, the `Property` and `Value` properties are used to specify when the trigger should fire—for example, `Property="IsMouseOver"` `Value="True"`. |
| `Setters` | As soon as the trigger fires, you can use `Setters` to define a collection of `Setter` elements to change values for properties. The `Setter` class defines the properties `Property`, `TargetName`, and `Value` for the object properties to change. |
| `EnterActions`, `ExitActions` | Instead of defining setters, you can define `EnterActions` and `ExitActions`. With both of these properties, you can define a collection of `TriggerAction` elements. `EnterActions` fires when the trigger starts (with a property trigger, when the `Property`/`Value` combination applies); `ExitActions` fires before it ends (just at the moment when the `Property`/`Value` combination no longer applies). Trigger actions that you can specify with these actions are derived from the base class `TriggerAction`, such as `SoundPlayerAction` and `BeginStoryboard`. With `SoundPlayerAction`, you can start the playing of sound. `BeginStoryboard` is used with animation, discussed later in this chapter. |

## MultiTrigger

A property trigger fires when a value of a property changes. If you need to set a trigger because two or more properties have a specific value, you can use `MultiTrigger`.

`MultiTrigger` has a `Conditions` property whereby valid values of properties can be specified. It also has a `Setters` property that enables you to specify the properties that need to be set. In the following example, a style is defined for `TextBox` elements such that the trigger applies if the `IsEnabled` property is `True` and the `Text` property has the value `Test`. Try it by typing Test into the blank text box. If both apply, the `Foreground` property of the `TextBox` is set to `Red` (code file `TriggerSamples/MultiTriggerWindow.xaml`):
