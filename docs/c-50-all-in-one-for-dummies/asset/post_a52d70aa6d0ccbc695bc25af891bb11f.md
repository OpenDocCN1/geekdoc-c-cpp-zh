
## Chapter 4: Practical WPF

## In This Chapter

- Using built-in and customized commands
- Writing adequate unit tests
- Working with the ViewModel

Even though WPF still supports the direct event handler wire up (For example, through the OnClick event), WPF introduces a much better mechanism for responding to user events. It significantly reduces the amount of code you have to write and adds testability to your application. Traditional event handling is all contained in the code-behind for your form, which is extremely difficult to test in an automated fashion.

Software patterns have been around for a long time, first brought to the forefront by the classic tome Design Patterns: Elements of Reusable Object Oriented Software (Addison-Wesley) by Erich Gamma, Richard Helm, Ralph Johnson, and John Vissides commonly referred to as the “Gang of Four.” Software has evolved, and many new patterns have been developed over the years. One of the most effective interface patterns for WPF is the ModelViewModel pattern (commonly referred to as ViewModel). Using the ViewModel pattern in your WPF applications will improve software reuse, testability, readability, maintainability, and most of the other “ilities” as well. (You run across other design patterns throughout this book.)

## Command Attention

The Command Pattern has been around since, well, forever, and you most likely use it every day. Copy and Paste commands are example implementations of the pattern built into Windows and most Windows applications. WPF provides a significant number of built-in commands and also for completely customized commands!

Traditional handling of user events (and still supported in WPF) is through an event handler. When the button on the Window is clicked, the code in the event handler (which has to be in the code-behind file) will execute. By placing this code is mixed with the user interface code, mixing concerns. To be fair, nothing in the framework makes one put the code in the code-behind; it just seems to always end up there (You can, of course, separate your business logic into classes outside of your code-behind.)

This gets compounded when additional UIElements are added to the window that needs to execute the same code. The common fix for this situation is to refactor the code in the original event handler out to a separate method and have the event handlers for the related UIElements call the new method. The new method can even be moved into the Business Layer, separating concerns and allowing for testability.

The other issue is one of user experience. Often menus and buttons need to be enabled or disabled based on the condition of the data (or some other/user action) in the Window. If the user has the option, he tends to click "active" items repeatedly, wondering why nothing is happening here. He is, after all, trained at birth to find holes in your application.

The command pattern as implemented in WPF cleanly and easily resolves issues.

## ICommand

ICommand (which is the base interface for all commands discussed here) defines two event handlers and one event (see Listing 4-1).

### Listing 4-1: ICommand Interface

```
bool CanExecute(object parameter);
void Execute(object parameter);
event EventHandler CanExecuteChanged
```

Perhaps the most powerful feature of WPF commands is the capability to determine at runtime if the controls they are bound to can execute (See the next section for a detailed discussion.) CanExecute is run by the SqlCommand whenever changes, the PropertyChanged or CollectionChanged events are raised, or on demand through code. If the event handler returns false, all UIElements bound to that command are disabled.

The Execute event handler contains the code that gets executed when the user action is processed or the command is executed through code.

The CanExecuteChanged event provides a mechanism to tie into the INotifyCollectionChanged and INotifyPropertyChanged event handlers to determine when CanExecute needs to be required.

## RoutedCommand versus RoutedUICommand

The only difference between the RoutedCommand and the RoutedUICommand is that the RouteUICommand adds a Text property used to decorate the bound controls uniformly. MenuItems picks up this property automatically and assigns it to the Header property. Buttons (and other UElements need a bit of binding kung fu, as the following XAML snippet, to get the Text into the Content property.)

```
Content={Binding
    RelativeSource={RelativeSource
    Mode=Self}, Path=Command.Text*}
```

## Routed commands

The ICommand interface doesn't provide the goodness of commands in WPF. The RoutedCommand class (and its first descendant, RoutedUICommand) takes advantage of event routing to provide additional power.

The CanExecute event raises the PreviewCanExecute event, and the Execute event raises the PreviewExecuted event. These events are raised just prior to the CanExecute and Execute handlers and bubble up the element tree until an element with the correct Command Binding is loaded. This is useful for allowing control of commands at a higher level while the fine-grained elements still control the CanExecute and the Execute event handlers.

Routed commands expose a collection of InputGestures or other gestures that will fire the Execute event. This allows assigning hot key combinations to the commands, such as Control+S for saving (as in Windows applications).

## Built-in commands

WPF has a number of built-in commands that you can use with very little (sometimes) no code. The most common set used by business developers is wrapped in the ApplicationCommands Library. The advantage of using the built-in commands is all that the plumbing is taken care of you. For example, the CanExecute and Execute event handlers are already implemented. All you have to do is bind them to UIE through XAML.

![](img/6df7bb88e9302e98442acc219cfbd7fc_650_0.png)

The full list of built-in commands is available online at http://microsoft.com/en-us/library/system.windows.input.aspx.

The sample shown in Listing 4-2 and Figure 4-1 uses the ApplicationCommands.Copy and ApplicationCommands.Paste commands to facilitate clipboard manipulation in your application. When the UIElement with focus supports the clipboard Paste action and there is data in the clipboard that is support by the element, any elements bound to the Paste command are enabled. When the UIElement with focus supports the clipboard Copy and there are items that can be copied to the clipboard, elements bound to them the Copy command are enabled. (See Figures 4-2 and 4-3.) As a side note, WPF allows you to abbreviate the built-in commands by dropping the container name (ApplicationCommands), so Copy and Paste are legitimate abbreviations for the command bindings ApplicationCommands.Copy and ApplicationCommands.Paste. For readability, I prefer to fully qualify the names.

The full code for the Command sample is in the project Chapter 4Commands and Chapter4CommandsTests in the Chapter 4 Solution.

### Listing 4-2: Built-in commands in XAML

```
<Menu Grid.Row="0" Grid.Column="0" HorizontalAlignment="Left" Name="menu">
  <MenuItem Command="ApplicationCommands.Copy/>
  <MenuItem Command="ApplicationCommands.Paste"/>
</Menu>
<TextBox Grid.Row="1" Grid.Column="0" HorizontalAlignment="Stretch"/>
<TextBox Grid.Row="2" Grid.Column="0" HorizontalAlignment="Stretch"/>
```

**Figure 4-1:**
Built-in commands (with empty clipboard and no selections).

![](img/6df7bb88e9302e98442acc219cfbd7fc_651_0.png)

**Figure 4-2:**
Built-in commands (with empty clipboard and text selection).

![](img/6df7bb88e9302e98442acc219cfbd7fc_651_1.png)

**Figure 4-3: Built-in commands (with clipboard data and no text selection).**

![](img/6df7bb88e9302e98442acc219_652_0.png)

## Focus!

I know the question you're dying to ask: If the user clicks a menu item, doesn't mean they then have focus? The answer is a confusing "No! That's because WPF work a little bit of magic to determine what UElement has focus before a menu item is clicked.

Unfortunately, this doesn't apply to standard buttons and other command controls. Even though the menu items in Figure 4-4 are enabled, the buttons are not. There are two fixes for this problem. The first is by binding the CommandTarget property in addition to the command to the UElement. This is a single element solution, though. To resolve the issue for all Elements, the FocusManager.IsSharedScope property needs to be set to True in the parent container.

**Figure 4-4: Built-in controls buttons.**

![](img/6df7bb88e9302e98442acc219cfbd7fc_652_1.png)

## Custom commands

Creating a custom command requires either instantiation of a new Routed[UI]Command or coding a new command based on the ICommand interface. Well, okay, you are correct — there are other ways as well. The two most popular are what I discuss here.

## Custom routed UI commands
