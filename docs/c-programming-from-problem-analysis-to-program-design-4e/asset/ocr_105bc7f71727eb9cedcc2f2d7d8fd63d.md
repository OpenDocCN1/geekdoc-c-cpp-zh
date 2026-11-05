parameters instead of having to worry about getting the exact order of which argument goes where when you call the method. You may also assign default values to parameters so that a call to the method does not need to send in a value unless it is different from the associated default value. While these features should probably be used sparingly, they are nice additions to the language and are discussed in the next sections.

# Default Values with Optional Parameters

When you assign a default value to a parameter, it then becomes an optional parameter. You do not have to send in a value every time you call the method. Instead the default value is used if no value is sent in as a parameter. You may have more than one optional parameter associated with a method. However, if you have more than one, the optional parameters must be placed last in the list of parameters, after any required parameters. Example 3-19 illustrates optional parameters with default values.

# EXAMPLE 3.19

```
public static void DoSomething(string name, int age = 21,
    bool currentStudent = true,
    string major = "CS")
{
    // additional program statements go here
}
```

You can now call DoSomething( ) and send in arguments for the default value or the default values will be assigned to the parameters. Example 3-20 shows valid calls to the DoSomething( ) method.

# EXAMPLE 3.20

```
DoSomething ("Elizabeth Abbott", 20);
DoSomething ("James Gabriel");
DoSomething ("Jonathan Byrle", 25, false, "MS");
```

Default values must be constants. If no arguments are sent for a particular parameter, the default value is used. One of the limitations on using optional parameters is if you need to send in arguments for any of the optional parameters, you must provide arguments for all preceding optional parameters. Thus, the call DoSomething ("Gabriella Henson", "MS"); is not a valid call, but DoSomething ("Joe Smith", 20, false); is a valid call. Notice it was not necessary to send a value for the major, but you need to send a boolean value for currentStudent, you must also send in values for all preceding parameters. In this case, you had to send a value for the optional parameter age.