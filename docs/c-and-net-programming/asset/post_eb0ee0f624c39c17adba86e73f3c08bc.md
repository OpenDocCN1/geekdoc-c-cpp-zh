
```xml
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
xmlns:local="clr-namespace:DropBoxIntegration" mc:Ignorable="d"
Title="MainWindow" Height="321" Width="1024" MinHeight="300" MinWidth="600">
<Grid>
    <Button x:Name="button" Content="Button"
        HorizontalAlignment="Left" Margin="273,3,0,0"
        Grid.Row="3" VerticalAlignment="Top" Width="75" Height="17" Click="Clicked">

        <x:Code>
            <![CDATA[
void Clicked(object sender, RoutedEventArgs e)
{
    MessageBox.Show("Hello World");
}
            ]]>
        </x:Code>
    </Button> </Grid>
</Window>
```

## 27.2 Bubbling and Tunneling Events and Events Pairing

In a Windows Forms application, a control raises an event and that is all required to process it further. WPF (Windows Presentation Foundation) uses more complicated **routed events** that are routed through a sequence of controls.

### 27.2.1 Bubbling and Tunneling Events

First the event **tunnels** down through the control hierarchy in a sequence of preview events. Then it bubbles back up through the control hierarchy in a sequence of final, possibly converted events.

All of the controls in the tunneling and bubbling chain can handle the event and take action. They can also set their **e.Handled** parameters to true to stop the event from continuing on its little adventure.

Below are the three routing strategies in WPF:

- **1. Direct events** – These are the events that are raised by a control and handled by that source control itself. These events are not at all traversed up or down the visual tree unlike other two types of events.
- **2. Bubbling events** – Events handlers in the source controls are handled by the handlers in the source control which successively is handled by the parent element and following the same strategy it travels up the visual tree until it reaches the element tree root.
- **3. Tunneling events** – Events handlers at the element tree root element, are invoked first and traverses down the visual element tree until it reaches the event element source that is the control at which the event originally occurred. These events start with the prefix Preview.

For example consider an application form that contains a main Grid control. At the top, that control contains another Grid that holds a StackPanel holding three Button controls. If the top-level **Grid** control is ignored, which doesn’t participate in the events used by this example, the hierarchy looks as shown in the Fig. 27.2.1,

![](img/3005a4307e6d8f3bb7e76eea28a92357_876_0.png)

When Button 1 is clicked, **PreviewMouseDown** events start at the **Grid** control and tunnel their way down the hierarchy until they reach the **button**. After that, Click events bubble up from the Button through the hierarchy to the Grid. Fig. 27.2.2 shows these events.

![](img/3005a4307e6d8f3bb7e76eea28a92357_876_1.png)

In the example program below the **CheckBox** controls can be used to make an event handler set its **e.Handled** parameter to **true** to interrupt the flow of events. For example, if the “Handle in Button.Preview” box is checked, then the last preview event flags its event as handled so none of the **Click** events occur.

Below is the XAML code that creates the first button,

```xml
<Button Name="Button1" Content="Button 1"
  PreviewMouseDown="Button1_PreviewMouseDown"
  Click="Button1_Click" />
```

This code creates the button and assigns event handlers to its **PreviewMouseDown** and **Click events**. The following code shows those event handlers,

```csharp
private void Button1_PreviewMouseDown(object sender,
    MouseButtonEventArgs e)
{
    e.Handled = chkHandleInButtonPreview.IsChecked.Value;
    ShowMethodName();
}

private void Button1_Click(object sender, RoutedEventArgs e)
{
    e.Handled = chkHandleInButtonClick.IsChecked.Value;
    ShowMethodName();
}
```

The event handlers set **e.Handled** appropriately depending on whether the corresponding check boxes are checked. They then call the following **ShowMethodName** method to record the name of the executing event handler.

```csharp
// Record the name of the method that called this one.
private void ShowMethodName()
{
    txtResults.AppendText(
        new StackTrace(1).GetFrame(0).GetMethod().Name + '\n');
}
```

The **ShowMethodName** adds the calling event handler's name to the text in the **txtResults** TextBox.

### 27.2.2 Event Pairing

Most of the bubbling events are paired with a Tunneling event. For example, the **PreviewKeyDown** (tunneling) key event is paired with the **KeyDown** event (bubbling). When the tunneling event works its way down the visual tree and hits the element (say a button) from whence it originated, if it is not handled there and then the button will kick off a "KeyDown" bubbling event that bubbles up the visual tree until it is handled itself (or not as the code may be). For example, **PreviewMouseDown** is paired with **MouseDown**, **PreviewMouseWheel** is paired with **MouseWheel** and so on.

## Two Marks Questions with Answers

### Q.1 What is XAML? What is the difference between XML and XAML?

**Ans.**: XAML stands for Extensible Application Markup Language. It is the language used to instantiate .NET objects. It is the language developed by Microsoft to write user interface for next generation applications.

XML is designed to store data or to work with the stored data, whereas XAML is the extended version of XML used for .NET programming.

### Q.2 Mention the advantage of using XAML.

**Ans.**: The advantages of using XAML:

- XAML code is clear to read, and they are short.
- Separation of designer code and logic.
- Tools like Expression Blend used for graphical design require XAML as source.
- It clearly separates the roles of designer and developer.
- XML Interview Questions

### Q.3 How can you code to display "Hello World" in XAML?

**Ans.**:

```
Displaying "Hello World."
<Page xmlns="">
<TextBlock>
Hello, World!
</TextBlock>
</Page>
```

### Q.4 What is attribute syntax in XAML?

**Ans.**: In XAML, attribute syntax sets a value for a property or names the event handler for an event, by declaring an attribute on an element. The attribute value should be enclosed within two quotation marks (").

For example:

```xml
<Button Background = "Black" Foreground = "Red" Content = "This is an operating button"/>
```

### Q.5 Explain content properties in XAML.

**Ans.**: XAML represents a language feature whereby a class can allot exactly one of its properties as XAML property.

### Q.6 What are the various x: prefixes used in XAML language?

**Ans.**:

- x: Key → It sets a unique key for each resource in a Resource Dictionary.
- x: Class → It specifies the CLR (Common Language Runtime) namespace and class name for the class that provides code.
- x: Name → It specifies a run-time object name for the instance that exists in run time code after an object element is processed.
- x: Static → It enables a reference that returns a static value which is otherwise an XAML-compatible property.
- x: Type → It constructs a Type reference based on the type name.

## Long Answer Questions

- Q.1 Discuss the concept of bubbling and tunneling and its use. (Refer section 27.2)
- Q.2 What is event pairing? (Refer section 27.2)
- Q.3 How objects are defined in XAML? (Refer section 27.1)
- Q.4 Discuss various XAML types. (Refer section 27.1)
- Q.5 Explain working and compilation of XAML. (Refer section 27.1)

*Core XAML, Reading and Writing XAML, Bubbling and Tunneling Events ends ...*

## Unit - V

## CHAPTER - 28

## .NET COMPACT FRAMEWORK - A COMPACT EDITION FOR SMART DEVICES

**Syllabus:** .NET Compact Framework, Compact Edition Data Stores, Errors, Testing and Debugging, Optimizing performance, Packaging and Deployment, Networking and Mobile Devices.

| Section No. | Topic Name | Page No. |
|---|---|---|
| 28.1 | .NET Compact Framework Fundamentals | 28 - 2 |
| 28.2 | Compact Edition Data Stores - SQL Server CE | 28 - 18 |
| 28.3 | .NET Compact Framework - Errors, Testing and Debugging | 28 - 19 |
| 28.4 | .NET Compact Framework - Optimizing Application Performance | 28 - 23 |
| 28.5 | .NET Compact Framework - Application Packaging and Deployment | 28 - 25 |
| 28.6 | .NET Compact Framework - Networking | 28 - 31 |
| 28.7 | .NET Compact Framework - Mobile Devices and Pocket PC Platform | 28 - 36 |
|  | Two Marks Questions with Answers | 28 - 39 |
|  | Long Answer Questions | 28 - 40 |
