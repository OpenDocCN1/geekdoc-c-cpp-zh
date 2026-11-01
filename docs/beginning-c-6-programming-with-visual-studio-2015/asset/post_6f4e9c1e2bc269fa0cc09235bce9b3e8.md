
## TRY IT OUT Manipulating Properties: Ch14Ex01\MainWindow.xaml

Return to the previous example and follow these steps. As you change the properties, notice how your changes affect the XAML and Design Views. You are going to change the window to look like Figure 14-1.

- 1. Start by selecting the second Button control in Design View; this is the button that is currently filling the entire window.
- 2. You can change the name of the control in the Properties panel at the very top. Change it to rotatedButton.
- 3. Under the Common node, change the Content to 2nd Button.
- 4. Under Layout, change width to 75 and height to 22.
- 5. Expand the Text node and change the text to bold by clicking the B icon.
- 6. Select the first button and drag it to a position above the second button. Visual Studio will assist with the positioning by snapping the control.

![](img/cf72ea860016d2d680fc085fc06f265a_441_0.png)

FIGURE 14-1

- 7. Select the second button again, and hover the mouse pointer over the top-left corner of it. The pointer changes to a quarter-circle with arrows on both ends. Drag down until the button is tilted down.
- 8. The XAML code for the window should now look like this:

```
<Window x:Class="Ch14Ex01.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:local="clr-namespace:Ch14Ex01"
    mc:Ignorable="d"
    Title="MainWindow" Height="350" Width="525">
<Grid>
    <Button x:Name="Button" Content="Button" HorizontalAlignment="Left"
        Margin="218,113,0,0" VerticalAlignment="Top" Width="75"/>
<Button x:Name="rotatedButton" Content="2nd Button" Width="75" Height="22" FontWeight="Bold" Margin="218,138,224,159" RenderTransformOrigin="0.5,0.5" >
<Button.RenderTransform>
<TransformGroup>
<ScaleTransform/>
<SkewTransform/>
<RotateTransform Angle="-23.896"/>
<TranslateTransform/>
</TransformGroup>
</Button.RenderTransform>
</Button>
</Grid>
</Window>
```

- 9. Run the application by pressing F5. Try to resize the window. Notice that the second button moves with the window, whereas the first button stays fixed.

## How It Works

Any change that you apply in any of the three views is reflected in the other views, but some things are easier to do in certain views. Changing something trivial like the text displayed on a button can be done quickly in XAML View, but adding the information needed to perform a render transformation is much quicker from Design View.

In this exercise, you began by changing the name of the button, which added the x:Name property to the button. The name of a control must be unique within the scope of the namespace, so you can use the name for only one control.

Next you changed the Content property, set the Height and Width of the control, and then changed the font to bold. Doing so changed the way the control displayed itself within the window. It used to fill all the space of its container, but now you have limited it to a specific size.

Then you dragged the first button to a specific position on the Design View. As you see later in this chapter, this action will not always yield the same results but is dependent on the container in which the control is placed. In this case, with the Grid container, the control can be dragged to a specific position. The action sets the Margin property on the control. Two other properties should be mentioned here: HorizontalAlignment="Left" and VerticalAlignment="Top". With these two properties set, the margin becomes relative to the top-left corner of the window and thus the control is pushed to the position you placed it in the grid. If you compare the first and second buttons at this point, you will notice that the second control has none of these properties set. By omitting the alignment properties as well as the margin properties, the control is placed at the center of the container, even at runtime. This means that the first button with the margin and alignments set is fixed when the window resizes, but the second button always stays centered.

Finally, you performed a little bit of a party trick. By dragging the control when the Rotate mouse pointer is displayed, you can rotate the control. This is a standard feature of XAML and WPF and can be applied to all controls, although there are a few controls that fail to change their content when the control itself is rotated. This includes controls that rely on Windows Forms or old Windows controls to display content.

```
VerticalAlignment="Top" Width="75" Grid.Column="0" Grid.Row="0"
Height="22" />
...
</Grid>
```

Here, the attached property is referred to using the name of the parent element, a period, and the name of the attached property.

In WPF, attached properties serve a variety of uses. You will see a lot of attached properties shortly, when you look at how to position controls in the “Control Layout” section. You will learn how container controls define attached properties that enable child controls to define, for example, which edges of the container to dock to.

## Events

In Chapter 13, you learned what events are and how to use them. This section covers particular kinds of events — specifically, the events generated by WPF controls — and introduces routed events, which are usually associated with user actions. For example, when the user clicks a button, that button generates an event indicating what just happened to it. Handling the event is the means by which the programmer can provide some functionality for that button.

Many of the events you handle are common to most of the controls that you work with in this book. This includes events such as LostFocus and MouseEnter. This is because the events themselves are inherited from base classes such as Control or ContentControl. Other events such as the CalendarOpened event of the DatePicker are more specific and only found on specialized controls. Some of the most used events are listed in Table 14-1.

TABLE 14-1: Common Control Events

| EVENT | DESCRIPTION |
|---|---|
| Click | Occurs when a control is clicked. In some cases, this event also occurs when a user presses the Enter key. |
| Drop | Occurs when a drag-and-drop operation is completed — in other words, when an object has been dragged over the control, and the user releases the mouse button. |
| DragEnter | Occurs when an object being dragged enters the bounds of the control. |
| DragLeave | Occurs when an object being dragged leaves the bounds of the control. |
| DragOver | Occurs when an object has been dragged over the control. |
| KeyDown | Occurs when a key is pressed while the control has focus. This event always occurs before KeyPress and KeyUp. |
| KeyUp | Occurs when a key is released while a control has focus. This event always occurs after KeyDown event. |

## TABLE 14-1 (continued)

| EVENT | DESCRIPTION |
|---|---|
| GotFocus | Occurs when a control receives focus. Do not use this event to perform validation of controls. Use Validating and Validated instead. |
| LostFocus | Occurs when a control loses focus. Do not use this event to perform validation of controls. Use Validating and Validated instead. |
| MouseDoubleClick | Occurs when a control is double-clicked. |
| MouseDown | Occurs when the mouse pointer is over a control and a mouse button is pressed. This is not the same as a Click event because MouseDown occurs as soon as the button is pressed and before it is released. |
| MouseMove | Occurs continually as the mouse travels over the control. |
| MouseUp | Occurs when the mouse pointer is over a control and a mouse button is released. |

You will see many of these events in the examples in this chapter.

## Handling Events

There are two basic ways to add a handler for an event. One way is to use the Events list in the Properties window, shown in Figure 14-2, which is displayed when you click the lightning bolt button.

![](img/cf72ea860016d2d680fc085fc06f265a_445_0.png)

FIGURE 14-2

To add a handler for a particular event, either type the name of the event and press Return, or double-click to the right of the event name in the Events list. This causes the event to be added to the XAML tag. The method signature to handle the event is added to the C# code-behind file.
