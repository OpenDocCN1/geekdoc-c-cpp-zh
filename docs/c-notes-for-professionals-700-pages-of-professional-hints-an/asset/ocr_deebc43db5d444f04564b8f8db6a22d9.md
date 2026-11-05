# Chapter 80: Diagnostics

# Section 80.1: Redirecting log output with TraceListeners

You can redirect the debug output to a text file by adding a TextWriterTraceListener to the Debug.Listeners collection.

```
public static void Main(string[] args)
{
    TextWriterTraceListener myWriter = new TextWriterTraceListener(@"debug.txt");
    Debug.Listeners.Add(myWriter);
    Debug.WriteLine("Hello");
    
    myWriter.Flush();
}
```

You can redirect the debug output to a console application's out stream using a ConsoleTraceListener.

```
public static void Main(string[] args)
{
    ConsoleTraceListener myWriter = new ConsoleTraceListener();
    Debug.Listeners.Add(myWriter);
    Debug.WriteLine("Hello");
}
```

# Section 80.2: Debug.WriteLine

Writes to the trace listeners in the Listeners collection when the application is compiled in debug configuration.

```
public static void Main(string[] args)
{
    Debug.WriteLine("Hello");
}
```

In Visual Studio or Xamarin Studio this will appear in the Application Output window. This is due to the presence of the default trace listener in the TraceListenerCollection.