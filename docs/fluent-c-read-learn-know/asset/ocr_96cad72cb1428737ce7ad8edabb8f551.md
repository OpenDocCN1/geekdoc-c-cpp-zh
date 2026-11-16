# HOOKING UP COMMANDS

There are a lot of objects involved in the commanding process, but there are only three steps to the process.
You can perform the steps in any order.

# SET THE COMMAND PROPERTY ON THE SOURCE

The ICommandSource interface exposes three properties: Command, CommandParameter
and CommandTarget; any widget that can act as a control source will expose these as simple
properties (they're actually dependency properties) that can be set in XAML or code:

```
<MyObject Command="Cut" />
or
MyObject.Command = ApplicationCommands.Cut;
```

You don't need to specify the class
in XAML if you're using one of
the pre-defined command classes, but
you will if you defined your own
command.

In most situations that's all you'll need to do, but you can also set the CommandParameter
and CommandTarget properties if you need to. The syntax is identical.

# WRITE THE HANDLERS

You'll need two. The handler for the CanExecute event needs to match the signature for the
CanExecuteRoutedEventHandler, which is

```
void <MethodName>(Object sender, CanExecuteRoutedEventArgs e)
```

By convention, the method is named <CommandName>CanExecute. It should set the
CanExecute property of the CanExecuteRoutedEventArgs to true or false to
reflect whether the command is available.

The delegate for the ExecutedRoutedEventHandler is:

```
. void <MethodName>(Object sender, ExecutedRoutedEventArgs e)
```

And by convention, it's named <CommandName>Executed. The handler performs the actual
logic of executing the command.