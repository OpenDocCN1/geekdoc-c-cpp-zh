Obviously, the generic `InArgument<>` and `OutArgument<>` types define the input and output arguments, respectively. The type parameters tell the type of the arguments — in this case, both of them are strings. When you run the workflow, the HelloWorkflow class is instantiated, and arguments are matched with the appropriate property by the names in the dictionary passed to the `Invoke` method.

> > Try to pass a wrong argument name in the Main method — for example, Msg instead of Message. You'll receive a System.ArgumentException with the message, "The values for the root activity's arguments do not satisfy the root activity's requirements."

# Declaring Variables

The HelloWorkflow constructor defines the `temp` local variable that is used as a workflow variable:

```
var temp = new Variable<string>("temp");
```

Although it contains data, it is not declared as a native string variable, but rather as `Variable<string>`. The "temp" argument used here tells the name of the variable. You may wonder why this is instead of using a native variable. The reason is that workflow instances can be persisted to storage when they are idle (for example, waiting for input). In this case, their state is represented by their variables. Without going into detail, this persistence requires that workflow variables can be referenced. Variable generic type provides this requirement. .NET reflection does not provide a way to retrieve local variable information for a method, so the "temp" name passed to the argument helps the workflow runtime to manage the distinction of variables. 

# Building Activities

The `Sequence` activity is defined like this:

```
new Sequence
{
    DisplayName = "Hello Workflow",
    Variables = { temp },
    Activities = {
        // ...
    }
}
```

The `DisplayName` property is the one you can set in the Properties window when using the workflow designer. The `Variables` container contains `Variable<>` instances that are taken into account as constituting the state of a workflow instance. The `Activities` container enumerates the nested activities of `Sequence` to execute in the order as they are listed.