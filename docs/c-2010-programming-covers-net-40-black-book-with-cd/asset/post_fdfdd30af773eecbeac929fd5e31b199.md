
You can also create your own routed events for an element and handle them. Routed events are instances of the RoutedEvent class; therefore, you need to first declare a public, static, and read-only field of RoutedEvent type. The routed event then needs to be registered with the WPF event system using the RegisterRoutedEvent() method of the EventManager class. After registering the routed event, you need to implement the add and remove CLR wrappers for it. The add and remove CLR wrappers use the AddHandler() and RemoveHandler() methods to allow event handling for the routed event. You will learn how to create custom routed events in the Immediate Solutions section of this chapter.

NOTE
The AddHandler() and RemoveHandler() methods are defined in the FrameworkElement class.

## Attached Events

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

- public, static, void—Represents the C# keywords

## Lifetime Events

Every element that you create or use in WPF application has its life. The lifetime of the elements is characterized by particular stages or events, such as when the elements are created or initialized, loaded, and destroyed. The events may vary depending on the actual element. However, there are certain events that are common to all the elements in WPF. The common events that characterize the lifetime of the elements in WPF are as follows:

- Initialized — Refers to the very first event that occurs in the lifetime of an element. This event is raised when an element is created and appropriately configured with the given properties (except for style, data binding, and dynamic resource properties). If an element contains a child element, then this event occurs first on the child element moving up to the parent element. This is because the parent element is not fully initialized and set, unless its child elements are initialized.

- Loaded — Refers to the second lifetime event that occurs after the Initialized event signals that all the elements (with their style and data binding properties) in the application is set and ready to be rendered. Note that the Loaded event first occurs at the root element (Window or Page) and then moves down to the child elements. The elements are considered to be loaded and can be rendered on the screen when the Loaded events are raised on them.

- Unloaded — Refers to the last lifetime event. This event occurs when an specific element, or its root element or parent element is removed from the WPF application.

> NOTE
> The lifetime events are available in the FrameworkElement class.

In addition to the common events that occur in the lifetime of the elements of WPF applications, there are events, such as window (Window element) and page (Page element) that are specific to the application. Let’s learn about these events starting first with the application specific lifetime events.

## Application Lifetime Events

The standalone WPF applications and XBAPs follow a particular sequence of events during their lifetime. The lifetime events for standalone WPF applications and XBAPs are somewhat different. The lifetime events of a standalone WPF application are as follows:

- Startup — Refers to the first event that occurs just after the Run() method is called for the application. The Startup event indicates that the application is ready to be displayed. In the event handler of the Startup event, you can create a Window object and specify it as the main window for the application. In addition, you can compute or process any command-line arguments for the application.

- Activated — Refers to the event that occurs when a standalone WPF application becomes the active application. An application is an active application when the window of the application appears on top of windows of other applications.

- Deactivated — Refers to the event that occurs when a standalone WPF application is no longer the active application or becomes inactive. In other words, when the window of the application goes in the background and is not the current window anymore, it is called the deactivated event.

- SessionEnding — Refers to the event that occurs when the application shuts down and the current user terminates the Windows session. For example, this event occurs if the user shuts down or restarts the computer or logs off from the session.

- Exit — Refers to the event that occurs just before the application shuts down. In the Exit event, you can specify any finalizing actions, such as saving the exit code.

> NOTE
> You can also use the RaiseEvent() method to raise the attached events for the desired occurrences in WPF applications.

Add<AttachedEventName>Handler — Represents the name of the add event accessor. The <AttachedEventName> is the name of the attached event. For example, if you have created an attached event named Resize, then the add event accessor is AddResizeHandler.

## NOTE

> In Chapter 3, Flow Control and Exception Handling in C# 2010 Programs, you learned how certain abnormal conditions known as exceptions abruptly halt the execution of the application. In WPF also, exceptions cause applications to shut down or stop executing. In such cases, if the exception remains unhandled, then the DispatcherUnhandledException event is raised. You can then handle the exception in the DispatcherUnhandledException event handler.

The XBAPs are mainly characterized by the Startup and Exit events and rest of the events, such as Activated, Deactivated, and SessionEnding, do not occur for XBAPs. When the Startup event occurs, the main page of the XBAP appears; whereas when the Exit event occurs the user navigates to some other page of XBAP or closes the Web browser. In case of any unhandled exceptions, the DispatcherUnhandledException event may also occur.

## NOTE

> The Application class defines the application lifetime events for both standalone WPF applications and XBAPs.

## Window Lifetime Events

As you know, the crux of standalone WPF applications is a window, which is an instance of the Window class. A standalone WPF application can have multiple windows. Each window in the application has a lifetime, which itself is characterized by a series of events.

- SourceInitialized – Refers to the event that occurs when the window is initialized, that is, when the standalone WPF application is initialized and its Startup event is raised. The SourceInitialized event signals that the window is ready to be displayed.

- Activated – Refers to the event that occurs when a window becomes the active window, that is, the window appears in front of other windows.

- Loaded – Refers to the event that occurs when a window and its properties are loaded and the window is all set to be rendered.

- ContentRendered – Refers to the event that occurs just after the window and its content (controls) is rendered. If the window does not have any content, then this event may not occur.

- Deactivated – Refers to the event that occurs when the current window becomes inactive, that is, when another window becomes the active window.

- Closing – Refers to the event that occurs when the user closes the window, for instance, by shutting down the application. This event occurs before the window is actually closed. You can include certain preventive or finalizing actions before the window is closed, such as cancelling the close operation of the window and saving any data. Note that if the user shuts down the computer or logs off while the window is open, then the Closing event is not raised.

- Closed – Refers to the event that occurs just before the window is closed. This event signals that the window would close in a while and there is no way to cancel the closing operation.

Similar to the windows in standalone WPF applications, a page in XBAPs has a life of its own. You may recall that a page in XBAPs is an instance of the Page class. In addition, the page is hosted in a Web browser or some other particular controls, such as window and frame. The users of the XBAP can navigate to the page in any random order. This implies that the lifetime of a page is subject to a lot of changes or events depending on its navigation status; therefore, it is not discussed in this chapter.

Let’s learn about dialog boxes in WPF applications.

## Working with Dialog Boxes in WPF Applications

Similar to Windows Forms applications, standalone WPF applications can also make use of dialog boxes for better user interactivity. You can use dialog boxes to incorporate functionalities in the WPF application to display or retrieve some information from the users. In WPF 4.0, dialog boxes can be of the following two types:

- Modal dialog box – Refers to a dialog box that remains visible unless explicitly closed. As long as a modal dialog box is opened, you cannot work with any other windows of the application. Modal dialog boxes are suitable for situations where you want to retrieve certain information from the users and utilize that
