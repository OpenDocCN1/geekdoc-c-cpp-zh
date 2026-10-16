
<RibbonApplicationMenuItem Header="Show _Book" />
<RibbonSeparator />
<RibbonApplicationMenuItem Header="Exit" Command="Close" />
</RibbonApplicationMenu>
</Ribbon.ApplicationMenu>

After the application menu, the content of the Ribbon control is defined by using RibbonTab elements. The title of the tab is defined with the Header property. The RibbonTab contains two RibbonGroup elements. Each of the RibbonGroup elements contains RibbonButton elements. With the buttons, you can set a Label to display text and either SmallImageSource or LargeImageSource properties for displaying an image:

```
<RibbonTab Header="Home">
    <RibbonGroup Header="Clipboard">
        <RibbonButton Command="Paste" Label="Paste" LargeImageSource="Assets/paste.png" />
        <RibbonButton Command="Cut" SmallImageSource="Assets/cut.png" />
        <RibbonButton Command="Copy" SmallImageSource="Assets/copy.png" />
        <RibbonButton Command="Undo" LargeImageSource="Assets/undo.png" />
    </RibbonGroup>
    <RibbonGroup Header="Show">
        <RibbonButton LargeImageSource="Assets/one.png" Label="Book" />
        <RibbonButton LargeImageSource="Assets/list.png" Label="Book List" />
        <RibbonButton LargeImageSource="Assets/grid.png" Label="Book Grid" />
    </RibbonGroup>
</RibbonTab>
```

The second RibbonTab demonstrates different controls that can be used within a ribbon control, for example, text box, check box, combo box, split button, and gallery elements. Figure 34.14 shows this tab open.

```
<RibbonTab Header="Ribbon Controls">
    <RibbonGroup Header="Sample">
        <RibbonButton Label="Button" />
        <RibbonCheckBox Label="Checkbox" />
        <RibbonComboBox Label="Combo1">
            <Label>One</Label>
            <Label>Two</Label>
        </RibbonComboBox>
        <RibbonTextBox>Text Box </RibbonTextBox>
        <RibbonSplitButton Label="Split Button">
            <RibbonMenuItem Header="One" />
            <RibbonMenuItem Header="Two" />
        </RibbonSplitButton>
        <RibbonComboBox Label="Combo2" IsEditable="False">
            <RibbonGallery SelectedValuePath="Content" MaxColumnCount="1" SelectedValue="Green">
                <RibbonGalleryCategory>
                    <RibbonGalleryItem Content="Red" Foreground="Red" />
                    <RibbonGalleryItem Content="Green" Foreground="Green" />
                    <RibbonGalleryItem Content="Blue" Foreground="Blue" />
                </RibbonGalleryCategory>
            </RibbonGallery>
        </RibbonComboBox>
```

```
</RibbonGallery>
</RibbonComboBox>
</RibbonGroup>
</RibbonTab>
```

![](img/3d365b72b289213a91ade7eb366b8f35_1319_0.png)

Figure 34.14

## Commanding

*Commanding* is a WPF concept that creates a loose coupling between the source of an action (for example, a button) and the target that does the work (for example, a handler method). This concept is based on the *Command* pattern from the Gang of Four. With WPF, events are strongly coupled. Compiling the XAML code that includes references to events requires that the code-behind have a handler implemented and available at compile time. With commands, the coupling is loose.

> NOTE The command pattern is a behavioral design pattern that makes unit testing easier by separating the client from the receiver of the command.

The action that is executed is defined by a command object. Commands implement the interface `ICommand`. Command classes that are used by WPF are `RoutedCommand` and a class that derives from it, `RoutedUICommand`. `RoutedUICommand` defines an additional `Text` property that is not defined by `ICommand`. This property can be used as textual information in the UI. `ICommand` defines the methods `Execute` and `CanExecute`, which are executed on a target object.

The *command source* is an object that invokes the command. Command sources implement the interface `ICommandSource`. Examples of such command sources are button classes that derive from `ButtonBase`, `Hyperlink`, and `InputBinding`. `KeyBinding` and `MouseBinding` are examples of `InputBinding` derived classes. Command sources have a `Command` property whereby a command object implementing `ICommand` can be assigned. This fires the command when the control is used, such as with the click of a button.

The command target is an object that implements a handler to perform the action. With command binding, a mapping is defined to map the handler to a command. Command bindings define what handler is invoked on a command. Command bindings are defined by the CommandBinding property that is implemented in the UIElement class. Thus, every class that derives from UIElement has the CommandBinding property. This makes finding the mapped handler a hierarchical process. For example, a button that is defined within a StackPanel that is inside a ListBox—which itself is inside a Grid—can fire a command. The handler is specified with command bindings somewhere up the tree —such as with command bindings of a Window. The next section changes the implementation of the BooksDemoRibbon project to use commands.

## Defining Commands

.NET gives you classes that return predefined commands. The ApplicationCommands class defines the static properties New, Open, Close, Print, Cut, Copy, Paste, and others. These properties return RoutedUICommand objects that can be used for a specific purpose. Other classes offering commands are NavigationCommands and MediaCommands. NavigationCommands is self-explanatory, providing commands that are common for navigation such as GoToPage, NextPage, and PreviousPage. MediaCommands are useful for running a media player, with Play, Pause, Stop, Rewind, and Record.

It’s not hard to define custom commands that fulfill application domain–specific actions. For this, the BooksCommands class is created, which returns RoutedUICommands with the ShowBook and ShowBooksList properties. You can also assign an input gesture to a command, such as KeyGesture or MouseGesture. In the following example, a KeyGesture is assigned that defines the key B with the Alt modifier. An input gesture is a command source, so clicking the Alt+B combination invokes the command (code file BooksDemoLib/Commands/BooksCommands.cs):

```
public static class BooksCommands
{
    private static RoutedUICommand s_showBook;
    public static ICommand ShowBook =>
        s_showBook ?? (s_showBook = new RoutedUICommand("Show Book",
            nameof(ShowBook), typeof(BooksCommands)));

    private static RoutedUICommand s_showBooksList;
    public static ICommand ShowBooksList
    {
        get
        {
            if (s_showBooksList == null)
            {
                s_showBooksList = new RoutedUICommand("Show Books",
                    nameof(ShowBooksList), typeof(BooksCommands));
                s_showBooksList.InputGestures.Add(new KeyGesture(Key.B,
                    ModifierKeys.Alt));
            }
        }

```
```
return s_showBooksList;
} 
// etc.
}
```

## Defining Command Sources

Every class that implements the ICommandSource interface can be a source of commands, such as Button and MenuItem. Inside the Ribbon control created earlier, the Command property is assigned to several RibbonButton elements—for example, in the quick access toolbar—as shown in the following code snippet (code file BooksDemoRibbon/MainWindow.xaml):

```
<Ribbon.QuickAccessToolBar>
< RibbonQuickAccessToolBar>
< RibbonButton SmallImageSource="Assets/one.png"
Command="local:BooksCommands.ShowBook" />
< RibbonButton SmallImageSource="Assets/list.png"
Command="local:BooksCommands.ShowBooksList" />
</RibbonQuickAccessToolBar>
</Ribbon.QuickAccessToolBar>
```

Predefined commands such as ApplicationCommands.Cut, Copy, and Paste are assigned to the Command property of RibbonButton elements as well. With the predefined commands the shorthand notation is used:

```
<RibbonGroup Header="Clipboard">
< RibbonButton Command="Paste" Label="Paste"
LargeImageSource="Images/paste.png" />
< RibbonButton Command="Cut" SmallImageSource="Images/cut.png"
/>
< RibbonButton Command="Copy"
SmallImageSource="Images/copy.png" />
< RibbonButton Command="Undo"
LargeImageSource="Images/undo.png" />
</RibbonGroup>
```

## Command Bindings

Command bindings need to be added to connect them to handler methods. In the following example, the command bindings are defined within the Window element so these bindings are available to all elements within the window. When the command ApplicationCommands.Close is executed, the OnClose method is invoked. When the command BooksCommands.ShowBooksList is executed, the OnShowBooksList method is called (code file BooksDemoRibbon/MainWindow.xaml):

```
<Window.CommandBindings>
<CommandBinding Command="Close" Executed="OnClose" />
<CommandBinding Command="commands:BooksCommands.ShowBooksList"
Executed="OnShowBooksList" />
</Window.CommandBindings>
```

With command binding you can also specify the CanExecute property, whereby a method is invoked to verify whether the command is
