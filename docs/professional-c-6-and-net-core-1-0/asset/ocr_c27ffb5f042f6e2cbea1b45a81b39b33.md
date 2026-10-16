```
return s_showBooksList;
} 
// etc.
}
```

# Defining Command Sources

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

# Command Bindings

Command bindings need to be added to connect them to handler methods. In the following example, the command bindings are defined within the Window element so these bindings are available to all elements within the window. When the command ApplicationCommands.Close is executed, the OnClose method is invoked. When the command BooksCommands.ShowBooksList is executed, the OnShowBooksList method is called (code file BooksDemoRibbon/MainWindow.xaml):

```
<Window.CommandBindings>
<CommandBinding Command="Close" Executed="OnClose" />
<CommandBinding Command="commands:BooksCommands.ShowBooksList"
Executed="OnShowBooksList" />
</Window.CommandBindings>
```

With command binding you can also specify the CanExecute property, whereby a method is invoked to verify whether the command is