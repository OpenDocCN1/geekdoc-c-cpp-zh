
## PUT ON YOUR THINKING HAT

Knowing the basic capabilities provided by FrameworkElement and Control gives you a head start on learning to use any of the WPF controls. Take the partial class diagrams below, for example. The DatePicker (which is like a combobox for displaying dates) and the Calendar (which is exactly what it sounds like) only expose properties and events that pertain to their own behavior. All the stuff that's common to all widgets is somewhere up the tree.

Using the class diagrams, can you write these C# and XAML snippets?

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_563_0.png)

- In C#, write an if statement that displays a MessageBox if the actual height of MyDatePicker is less than the requested height.
- In XAML, define a Calendar that displays its text using the Times New Roman FontFamily.
- In C#, use a MessageBox to display the Name property of MyCalendar.
- In C#, write a function that changes the background color of any control to the Beige static property of the Colors class.
- In XAML, define a DatePicker that has a Foreground color of AliceBlue.

## HOW'D YOU DO?

Were you surprised that you knew so much about these two controls?

In C#, write an if statement that displays a MessageBox if the actual height of MyDatePicker is less than the requested height.

```
if (MyDatePicker.ActualHeight < MyDatePicker.Height)
    MessageBox.Show("Didn't get as much as I asked for");
```

In XAML, define a Calendar that displays its text using the Times New Roman FontFamily.

```
<Calendar FontFamily="Times New Roman" />
```

In C#, use a MessageBox to display the Name property of MyCalendar.

```
MessageBox.Show(MyCalendar.Name);
```

In C#, write a function that changes the background color of any control to the Beige static property of the Brushes class.

```
void ChangeBackground(Control ctrl)
{
    ctrl.Background = Brushes.Beige;
}
```

The Brushes class is implemented in System.Windows.Media. It defines the standard colors as static properties. XAML knows what you mean if you just refer to the color name, but in C#, you have to reference the class itself.

In XAML, define a DatePicker that has a Foreground color of AliceBlue.

```
<DatePicker Foreground="AliceBlue" />
```

## ON YOUR OWN

Do you know (or can you guess) what all the members of the classes shown in the diagram represent? If there are any that seem obscure, check them out in MSDN.

## CONTENT CONTROLS

One of the most important branches of the WPF control class hierarchy is represented by the content controls that descend, appropriately enough, from ContentControl. Unlike a panel, which can contain multiple children, a content control can contain a single piece of content, but that content can be of any type (even a panel).

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_565_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_565_1.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_565_2.png)

The Content property is writable, so you won't usually need to use the AddChild() or AddText() methods, but they're called behind the scenes by the XAML interpreter.

## THE WINDOW

One very important, and slightly odd, content control is the Window. How is it odd? Glad you asked. The Window is odd because it's the only control that can't be hosted inside another control. That makes sense if you think about how UIs work (how could you put a Window inside a Button?) but it does violate strict OOP since it adds restrictions that don't exist in the parent (ContentControl).

AllowsTransparency lets you create non-rectangular windows. How cool is that?

To return a result from a Window opened with ShowDialog(), you set the DialogResult property before you call Close().

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_566_0.png)

OwnedWindows and Owner let you create applications with multiple windows.

The ShowDialog() method opens a window modally, which means that the user can't interact with the application until that window is closed. (The MessageBox is a modal window.) Such windows are called dialogs, and along with the DialogResult property, they let you create a dialog window that asks the user a question.

The Show() method displays a "normal", non-modal window that is displayed in the Windows Task Bar.

## PUT ON YOUR THINKING HAT

Here's a real challenge for you. Can you create the little application shown below? This is a pretty typical programming situation: You know what you need to do, and you know it's possible, but you're not entirely sure how to go about it. So you look at the objects, examine their properties and methods, maybe check around for some sample code somewhere. (Looking at sample code isn't cheating. Every programmer I know looks at sample code A LOT. That's why there are so many programming "cookbooks" on the market.)

When the window opens, it displays DateTime.Today in this label. [Hint: get the Content in the window constructor.]

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_567_0.png)

This is the main application window. It has a ThreeDBorderWindow style and displays a re-size grip. It always opens in the center of the screen. This is a re-size grip. The child (owned) window has a SingleBorderWindow style and can't be re-sized.

Clicking one of the buttons opens another window.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_567_1.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_567_2.png)

The window opened with ShowDialog() has a ToolWindow style. It doesn't display in the Windows task bar, can't be re-sized and always stays on top of any other window.

These buttons set the DialogResult to true or false, respectively, and then close the window. The DialogResult is displayed in a MessageBox by the main window.

Clicking the button displays the window's Owner.Title in a MessageBox.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_567_3.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_567_4.png)

## HOW'D YOU DO?

I warned you this one would be a challenge, so don't feel bad or stupid if it took you a while to work it all out.

Let's start with the basic window layouts. Here's the XAML that sets the properties of each window.

### MAIN APPLICATION WINDOW

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_568_0.png)

```
<Window x:Class="_15app07.MainWindow"
    WindowStyle="ThreeDBorderWindow"
    WindowStartupLocation="CenterScreen"
    ResizeMode="CanResizeWithGrip">
```

### DIALOG WINDOW

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_568_1.png)

```
<Window x:Class="_15app07.DialogWindow"
    WindowStyle="ToolWindow"
    ResizeMode="NoResize"
    ShowInTaskbar="False"
    Topmost="True">
```

### CHILD WINDOW

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_568_2.png)

```
<Window x:Class="_15app07.ChildWindow"
    ResizeMode="NoResize"
    WindowStyle="SingleBorderWindow">
```

## THE MAIN WINDOW

The main window displays the date when it opens. That code goes in the constructor.

```
public MainWindow()
{
    InitializeComponent();
    this.TodaysDate.Content = DateTime.Today;
}
```

## HANDLING THE DIALOG

To open a window as a dialog, you use the ShowDialog() method, and you have to capture the result in a nullable Boolean. (It has to be nullable because not all windows will return a result.)

You could also have declared this using the syntactic sugar bool? which is what IntelliSense shows you as the return value from ShowDialog().

```
private void OpenDialog_Click(object sender,
    RoutedEventArgs e)
{
    DialogWindow dw = new DialogWindow();
    Nullable<bool> result = dw.ShowDialog();
    MessageBox.Show(result.ToString());
}
```

The buttons on the dialog need to set the DialogResult using code like this.

```
private void OkButton_Click(object sender,
    RoutedEventArgs e)
{
    this.DialogResult = true;
    this.Close();
}
```

```
private void CancelButton_Click(object
    sender,
    RoutedEventArgs e)
{
    this.DialogResult = false;
    this.Close();
}
```

The code for the child window is on the next page...

## HOW'D YOU DO, CONTINUED...

Here's the last bit, the child window.

To open a child window, you simply set the Owner property before you open it.

```
private void OpenChild_Click(object sender,
    RoutedEventArgs e)
{
    ChildWindow cw = new ChildWindow();
    cw.Owner = this;
    cw.Show();
}
```

Finally, the button on the child window simply displays the Owner.Title property:

```
private void ShowOwner_Click(object sender,
    RoutedEventArgs e)
{
    MessageBox.Show(this.Owner.Title);
}
```

## TAKE A BREAK

Whew, that was a big exercise, wasn't it? Probably took you a while to put together. I've been doing this since before .NET was officially released, and it took me a while, so don't feel like you're struggling. But after all that hard work, why don't you take a break before we move on?
