# Debugging Techniques

The TraceTest class defines a private TraceSwitch member, sw, which controls what level of debug output is displayed. Each of the three member functions also calls the Debug::WriteLine() function to issue a debug message depending on the level set in the sw member of the class.

The FunA() function increments the value member of the class object each time it is called and the FunC() function asserts if value exceeds 3.

In main() you create a TextWriterTraceListener object that directs trace and debug output to the command line:

```
TextWriterTraceListener^ listener = gcnew TextWriterTraceListener( Console::Out);
```

You then add the listener object to the collection of listeners in the Debug class:

```
Debug::Listeners->Add(listener);
```

This causes debug and trace output to be directed to Console::Out, the standard output stream.

You create an array of TraceLevel objects that represent various control levels for debug and trace output:

```
array<TraceLevel>^ levels = { TraceLevel::Off,    TraceLevel::Error,
                           TraceLevel::Warning ,TraceLevel::Verbose};
```

After creating the TraceLevel object you set the trace levels for it in a for each loop:

```
for each(TraceLevel level in levels)
{
    obj->Level = level;                    // Set level for messages
    Console::WriteLine(L"\nTrace level is {0}", obj->Level);
    obj->FunA();
}
```

The level is set through the Level property for obj. This sets the Level property in the TraceSwitch member, sw, that is used in the instances functions to control output.

From the output you can see that the indent you set affects output from the static WriteLine() function in both the Debug and Trace classes. You can also see how the level that you set in the TraceSwitch class member affects the output. When the value member of the TraceTest class object, obj, reaches 4, the FunC() function asserts. You can rerun the example and try out the effects of the three buttons on the assertion dialog.

# Summary

Debugging is a big topic and Visual C++ 2005 provides many debugging facilities beyond what I have discussed here. If you are comfortable with what I have covered in this chapter, you should have little trouble expanding your knowledge of the debug capabilities through the Visual C++ 2005 documentation. Searching on “debugging” should generate a rich list of further information.