```
</RibbonGallery>
</RibbonComboBox>
</RibbonGroup>
</RibbonTab>
```

![](bbox=[0.1, 0.13, 0.89, 0.36])

Figure 34.14

# Commanding

*Commanding* is a WPF concept that creates a loose coupling between the source of an action (for example, a button) and the target that does the work (for example, a handler method). This concept is based on the *Command* pattern from the Gang of Four. With WPF, events are strongly coupled. Compiling the XAML code that includes references to events requires that the code-behind have a handler implemented and available at compile time. With commands, the coupling is loose.

> NOTE The command pattern is a behavioral design pattern that makes unit testing easier by separating the client from the receiver of the command.

The action that is executed is defined by a command object. Commands implement the interface `ICommand`. Command classes that are used by WPF are `RoutedCommand` and a class that derives from it, `RoutedUICommand`. `RoutedUICommand` defines an additional `Text` property that is not defined by `ICommand`. This property can be used as textual information in the UI. `ICommand` defines the methods `Execute` and `CanExecute`, which are executed on a target object.

The *command source* is an object that invokes the command. Command sources implement the interface `ICommandSource`. Examples of such command sources are button classes that derive from `ButtonBase`, `Hyperlink`, and `InputBinding`. `KeyBinding` and `MouseBinding` are examples of `InputBinding` derived classes. Command sources have a `Command` property whereby a command object implementing `ICommand` can be assigned. This fires the command when the control is used, such