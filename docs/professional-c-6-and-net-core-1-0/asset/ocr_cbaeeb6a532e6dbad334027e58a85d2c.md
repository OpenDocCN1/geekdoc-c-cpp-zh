as with the click of a button.

The command target is an object that implements a handler to perform the action. With command binding, a mapping is defined to map the handler to a command. Command bindings define what handler is invoked on a command. Command bindings are defined by the CommandBinding property that is implemented in the UIElement class. Thus, every class that derives from UIElement has the CommandBinding property. This makes finding the mapped handler a hierarchical process. For example, a button that is defined within a StackPanel that is inside a ListBox—which itself is inside a Grid—can fire a command. The handler is specified with command bindings somewhere up the tree —such as with command bindings of a Window. The next section changes the implementation of the BooksDemoRibbon project to use commands.

# Defining Commands

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