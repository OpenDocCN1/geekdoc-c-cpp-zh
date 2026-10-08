
```csharp
return value;
}
}
public FlashMode FlashMode
{
    get
    {
        FlashMode value = FlashMode.FlashDidNotFire;
        if (this.flashMode.HasValue && this.flashMode % 2 == 1)
        {
            value = FlashMode.FlashFired;
        }
        return value;
    }
}
public LightSource LightSource
{
    get
    {
        LightSource value = Exif.LightSource.Unknown;
        if (this.lightSource.HasValue
            && !String.IsNullOrWhiteSpace(Enum.GetName(typeof(LightSource), this.lightSource)))
        {
            value = (LightSource)this.lightSource;
        }
        return value;
    }
}
```

- 3. Add a private field to the `Photo` class named `metadata` and whose data type is `PhotoViewer.Exif.ExifMetadata`. Add a read-only property to the interface and the class that returns the metadata field.

## HOUR 6

### Events and Event Handling

**What You’ll Learn in This Hour:**

- Understanding Events
- Subscribing and Unsubscribing
- Publishing an Event
- Raising an Event

C# is inherently an imperative programming language, which enables you to describe how to accomplish tasks using procedures (methods). Procedural programming defines the exact statements that will be executed and the order in which they will be executed. This type of programming is most often found in command-line or non-interactive programs because of the generally limited amount of user interaction.

In contrast, event-driven programming is a programming style in which the program flow is determined by events. Events are simply anything of interest, such as user actions (mouse clicks or key presses) or messages from other programs or parts of the same program. In C#, the class that raises, or sends, the event is the **publisher**, and the classes that receive, or handle, the event are **subscribers**. Although you can use events for a variety of reasons, they are most commonly used to signal user actions in a graphical user interface, such as keyboard-related events (keys pressed) and mouse-related events (mouse movement, button clicks, and so on).

In this hour, you learn the basics of event-driven programming, including how to define your own events, initiate and respond to events, and send data through events.

### Understanding Events

Events follow a publish/subscribe model where the publisher determines when an event is raised. The subscribers determine the action taken in response to that event. Events can have multiple subscribers, in which case the event handlers are invoked synchronously when the event is raised. If an event has no subscribers, it is never actually raised. Subscribers can handle multiple events from multiple publishers.

> **By the Way**
>
> **Delegates**
>
> In traditional programming terms, an event is a form of a callback, which enables a method to be passed as an argument to other methods. In C#, these callbacks are referred to as delegates. Event handlers are actually nothing more than methods invoked through delegates.
>
> You can think of delegates as being similar to C or C++ function pointers or Delphi closures and are a type-safe and secure means of writing a callback. Delegates run under the caller's security permissions, not the declarer's permissions. A delegate type simply defines a method signature and any method with a compatible signature can be associated with a delegate. One key difference between delegate signatures and regular method signatures is that the return type is included in the signature and the use of the params modifier in the parameter list is allowed.

### Subscribing and Unsubscribing

When you are interested in responding to an event published by another class, you subscribe to that event by defining an event handler method whose signature matches the event delegate signature. You then use the addition assignment operator (`+=`) to attach the event handler to the event. Listing 6.1 shows how you would subscribe to an event based on the `ElapsedEventHandler` delegate.

**LISTING 6.1 Subscribing to an Event**

```csharp
var timer = new Timer(1000);
timer.Elapsed += new ElapsedEventHandler(TimerElapsedHandler);

void TimerElapsedHandler(object sender, ElapsedEventArgs e)
{
    MessageBox.Show("The timer has expired.");
}
```

The first parameter should always be an object parameter named `sender` that represents the object that raised the event. The second parameter represents the data passed to the event handler method. This is always an `EventArgs` type or a type derived from `EventArgs` named `e`. The event handler method should always have a void return type.

**Method Group Inference**

Although the code shown in Listing 6.1 is the traditional way to attach an event handler method, C# enables you to use a simpler syntax called method group inference. The code shown in Listing 6.1 is shown here but uses method group inference:

```csharp
var timer = new Timer(1000);
timer.Elapsed += TimerElapsedHandler;

void TimerElapsedHandler(object sender, EventArgs e)
{
    MessageBox.Show("The timer has expired.");
}
```

Even though Visual Studio automatically generates event handler attachments using the more traditional syntax, it is common to use method group inference when attaching your own event handler methods.

The method name can be anything you want, but it is best to be consistent and use a name that is the combination of the name of the object providing the event, the name of the event being handled, and the word Handler.

Although subscribing to events in this manner is common for many classes, Visual Studio makes it easy to subscribe to events, especially those published by any of the user interface controls.

These steps show how to subscribe to a button's Click event in a Windows Presentation Foundation (WPF) application:

- 1. Make sure the button is selected and click the Events tab on the top of the Properties window in Design view, as shown in Figure 6.1. If you don't see the Properties window, right-click the form or control to which you are going to handle an event and select Properties.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_153_0.png)

**FIGURE 6.1**
The Properties window

- 2. Double-click the event you will be handling. This causes Visual Studio to create an empty event handler method in your code, shown in Figure 6.2.

**FIGURE 6.2**
The generated event handler method

```csharp
private void button1_Click(object sender, RoutedEventArgs e)
{
    
}
```

Visual Studio also attaches the event handler for you, as shown in Figure 6.3. For WPF applications, this is done in the XML markup, or XAML, which describes the control.

**FIGURE 6.3**
Attaching the event handler in XAML

```xml
<Window x:Class="EventsWpf.MainWindow"
       xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
       xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
       Title="MainWindow" Height="350" Width="525">
    <Grid>
        <Button Content="Button" Click="button1_Click" Height="23" />
    </Grid>
</Window>
```

If you create a Windows Forms-based application, the process is similar but instead of attaching the event handler in the XAML, Visual Studio would attach the event handler in the `InitializeComponent` method of your form, as shown in Figure 6.4.

**FIGURE 6.4**
Attaching the event handler in code

```csharp
this.button1.Text = "Button1";
this.button1.UseVisualStyleBackColor = true;
this.button1.Click += new System.EventHandler(this.button1_Click);
```

When you double-click the event, Visual Studio uses a default naming convention. If you want to use a different event handler method name, simply type the name in the text area next to the event, and press the Enter key to cause Visual Studio to create the event handler method. If you double-click the control itself rather than the event, Visual Studio creates an event handler method for the default event of the control.

### Subscribing to Events

To subscribe to events published by a user interface control in a Windows Forms application and a WPF application, follow these steps.

- Open the Hour6 solution in Visual Studio.
- Open Form1.cs in the EventsWinForms project by double-clicking the file.
- In the design view for Form1, select the button and add an event handler for the Click event.
- In the generated event handler method, add the following statement:

```csharp
MessageBox.Show("You pressed the button.");
```

- Run the application by pressing Ctrl+F5. When you click the button, you should see the following dialog appear, as shown in Figure 6.5.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_155_0.png)

**FIGURE 6.5**
Message box from the event handler

- Open MainWindow.xaml in the EventsWpf project by double-clicking the file.
- In the design view for MainWindow, select the button and add an event handler for the Click event. In the generated event handler method, add the same statement you added in step 4.
- Run the application by right-clicking the project in the Solution Explorer window and selecting the Start new instance option from the Debug menu, as shown in Figure 6.6.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_155_1.png)

**FIGURE 6.6**
Solution Explorer context menu

- When you click the button, you should see the following dialog appear, as shown in Figure 6.7.
