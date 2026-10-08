```
}
```

```
public void voidQueryStatus(string commandName,
vsCommandStatusTextWanted neededText,
ref vsCommandStatus status,
ref object commandText)
{
    if (neededText == vsCommandStatusTextWanted.vsCommandStatusTextNone)
    {
        if (commandName == "MySimpleAddIn.Connect.MySimpleAddIn")
        {
            status = (vsCommandStatus)vsCommandStatus.vsCommandStatusSupported |
                vsCommandStatus.vsCommandStatusEnabled;
            return;
        }
    }
}
ublic void Exec(string commandName, vsCommandExecution executeOption,
ref object varIn, ref object varOut, ref bool handled)
{
    handled = false;
    if (executeOption == vsCommandExecution.vsCommandExecutionOptionDoDefault)
    {
        if (commandName == "MySimpleAddIn.Connect.MySimpleAddIn")
        {
            MessageBox.Show("Hello from MySimpleAddIn");
            handled = true;
        }
    }
}
private DTE2 _applicationObject;
private AddIn _addInInstance;
```

Let's dive into its details of this code. To understand every bit, you must understand a lot of information about the command-handling mechanism of Visual Studio. Treating all those details would at least double the length of this chapter, let's focus on a general overview of what the code does. If you want to look deeper behind the source code, use the reference documentation for the methods, parameters, and types.

The Connect class implements the IDExtensibility2 and IDCommandTarget interfaces. Both are COM interfaces, so as a result, the Connect class is an OBJ that can be integrated with Visual Studio 2010. IDExtensibility2 is responsible for the IDE integration. IDCommandTarget enables the IDE to send commands to the add-in. IDExtensibility2 defines the methods summarized in Table 6-3. All methods have an array parameter custom that can be used to pass data back to the caller.