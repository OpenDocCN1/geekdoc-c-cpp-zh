# Lifetime Events

Every element that you create or use in WPF application has its life. The lifetime of the elements is characterized by particular stages or events, such as when the elements are created or initialized, loaded, and destroyed. The events may vary depending on the actual element. However, there are certain events that are common to all the elements in WPF. The common events that characterize the lifetime of the elements in WPF are as follows:

+   - Initialized — Refers to the very first event that occurs in the lifetime of an element. This event is raised when an element is created and appropriately configured with the given properties (except for style, data binding, and dynamic resource properties). If an element contains a child element, then this event occurs first on the child element moving up to the parent element. This is because the parent element is not fully initialized and set, unless its child elements are initialized.

+   - Loaded — Refers to the second lifetime event that occurs after the Initialized event signals that all the elements (with their style and data binding properties) in the application is set and ready to be rendered. Note that the Loaded event first occurs at the root element (Window or Page) and then moves down to the child elements. The elements are considered to be loaded and can be rendered on the screen when the Loaded events are raised on them.

+   - Unloaded — Refers to the last lifetime event. This event occurs when an specific element, or its root element or parent element is removed from the WPF application.

> NOTE
> The lifetime events are available in the FrameworkElement class.

In addition to the common events that occur in the lifetime of the elements of WPF applications, there are events, such as window (Window element) and page (Page element) that are specific to the application. Let’s learn about these events starting first with the application specific lifetime events.

# Application Lifetime Events

The standalone WPF applications and XBAPs follow a particular sequence of events during their lifetime. The lifetime events for standalone WPF applications and XBAPs are somewhat different. The lifetime events of a standalone WPF application are as follows:

+   - Startup — Refers to the first event that occurs just after the Run() method is called for the application. The Startup event indicates that the application is ready to be displayed. In the event handler of the Startup event, you can create a Window object and specify it as the main window for the application. In addition, you can compute or process any command-line arguments for the application.

+   - Activated — Refers to the event that occurs when a standalone WPF application becomes the active application. An application is an active application when the window of the application appears on top of windows of other applications.

+   - Deactivated — Refers to the event that occurs when a standalone WPF application is no longer the active application or becomes inactive. In other words, when the window of the application goes in the background and is not the current window anymore, it is called the deactivated event.

+   - SessionEnding — Refers to the event that occurs when the application shuts down and the current user terminates the Windows session. For example, this event occurs if the user shuts down or restarts the computer or logs off from the session.

+   - Exit — Refers to the event that occurs just before the application shuts down. In the Exit event, you can specify any finalizing actions, such as saving the exit code.

> NOTE
> You can also use the RaiseEvent() method to raise the attached events for the desired occurrences in WPF applications.

Add<AttachedEventName>Handler — Represents the name of the add event accessor. The <AttachedEventName> is the name of the attached event. For example, if you have created an attached event named Resize, then the add event accessor is AddResizeHandler.