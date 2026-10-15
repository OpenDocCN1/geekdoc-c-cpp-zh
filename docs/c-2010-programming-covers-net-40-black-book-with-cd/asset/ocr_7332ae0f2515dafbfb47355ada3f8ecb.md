You can also create your own routed events for an element and handle them. Routed events are instances of the RoutedEvent class; therefore, you need to first declare a public, static, and read-only field of RoutedEvent type. The routed event then needs to be registered with the WPF event system using the RegisterRoutedEvent() method of the EventManager class. After registering the routed event, you need to implement the add and remove CLR wrappers for it. The add and remove CLR wrappers use the AddHandler() and RemoveHandler() methods to allow event handling for the routed event. You will learn how to create custom routed events in the Immediate Solutions section of this chapter.

NOTE
The AddHandler() and RemoveHandler() methods are defined in the FrameworkElement class.

# Attached Events

Similar to attached properties, attached events are the events that are owned or created in one element or class, however, they can be handled by other elements in the elements tree. Many of the input events, such as mouse and keyboard events, are attached events that are defined for every element in WPF.

Attached events are useful when you want to provide information about the compositing state of a child element to the parent element. The parent element can handle an event that is defined by a child element. This way if the child elements share the attached event and if the event is raised on any one of them, then the event handler can be specified only once in the parent element. This saves you from specifying the event handler for the same event in all the child elements. You can specify the handler for an attached event in the parent element by qualifying them with the name of the owner. For example, the Click event is an attached event, which is owned by the ButtonBase class, and it is inherited by its derived classes and elements, such as the Button and ToggleButton classes. Consider the following code snippet:

```
<Grid Name="grid1" ButtonBase.Click="button_click">
<Button Height="25" Name="button1" VerticalAlignment="Top" Margin="90,30,0,0">Button1</Button>
<ToggleButton Height="25" Name="toggleButton1" VerticalAlignment="Center">ToggleButton1</ToggleButton>
<Button Height="25" Name="button2" VerticalAlignment="Bottom" Margin="90,0,90,30">Button2</Button>
</Grid>
```

In the preceding code snippet, the Click event is associated with its handler in the Grid element that is the parent element for two Button elements named button1 and button2 as well as a ToggleButton element named toggleButton1.

Note that a handler for the Click event is specified in the Grid element by qualifying the event attribute (Click) with the name of the class (ButtonBase) that owns the event. The owner and the event name in the Grid element are separated by the dot operator. The event handler is called whenever any of the button or toggle button in the grid is clicked. In fact, if any element that derives from the ButtonBase class is added to the grid and if any of those elements is clicked, then the same event handler is called. In this way, you can have a common event handler for child elements. Note that though the Grid element does not itself define a Click event, it handles the Click event of its child elements that are derived from the ButtonBase class.

Attached events are fundamentally routed events and instances of the RoutedEvent class. In addition, these events are registered with the RegisterRoutedEvent() method. However, attached events do not have the CLR add and remove event wrappers to add and remove handlers, respectively. Instead, attached events use two public static methods to add and remove the event handlers. The syntax of the public static method that adds a handler for an attached event is as follows:

```
public static void Add<AttachedEventName>Handler()
{
    //add event handler logic
}
```

In the preceding syntax:

+   - public, static, void—Represents the C# keywords