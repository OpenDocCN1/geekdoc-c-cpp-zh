# Trace Sources

You can write trace messages with the TraceSource class. Tracing requires the Trace flag of the compiler settings. With a Visual Studio project, the Trace flag is set by default with debug and release builds, but you can change it through the Build properties of the project.

To write trace messages, you need to create a new TraceSource instance. In the constructor, the name of the trace source is defined. The method TraceInformation() writes an information message to the trace output. Instead of just writing informational messages, the TraceEvent() method requires an enumeration value of type TraceEventType to define the type of the trace message. TraceEventType.Error specifies the message as an error message. You can define it with a trace switch to see only error messages. The second argument of the TraceEvent() method requires an identifier. The ID can be used within the application itself. For example, you can use id 1 for entering a method and id 2 for exiting a method. The method TraceEvent() is overloaded, so the TraceEventType and the ID are the only required parameters. Using the third parameter of an overloaded method, you can pass the message written to the trace. TraceEvent() also supports passing a format string with any number of parameters in the same way as Console.WriteLine(). TraceInformation() does nothing more than invoke TraceEvent() with an identifier of 0. TraceInformation() is just a simplified version of TraceEvent(). With the TraceData() method, you can pass any object, for example, an exception instance, instead of a message. To make sure that data is written by the listeners and does not stay in memory, you need to do a Flush(). If the source is no longer needed, you can invoke the Close() method that closes all listeners associated with the trace source. Close() does a Flush() as well.

```
```csharp
public class Program
{
    internal static TraceSource trace =
        new TraceSource("Wrox.ProCSharp.Instrumentation");

    static void TraceSourceDemo()
    {
        trace.TraceInformation("Info message");

        trace.TraceEvent(TraceEventType.Error, 3, "Error message");
        trace.TraceData(TraceEventType.Information, 2, "data1", 4, 5);
        trace.Flush();
        trace.Close();
    }
}
```
```

code snippet TracingDemo/Program.cs

> *You can use different trace sources within your application. It makes sense to define different sources for different libraries, so that you can turn on different trace levels for different parts of your application. To use a trace source, you need to know its name. A commonly used name for the trace source is the same name as the assembly name.*

The TraceEventType enumeration that is passed as an argument to the TraceEvent() method defines the following levels to specify the severity of the problem: Verbose, Information, Warning, Error, and Critical. Critical defines a fatal error or application crash; Error defines a recoverable error. Trace messages at the Verbose level give you detailed debugging information. TraceEventType also defines action levels Start, Stop, Suspend, and Resume. These levels define timely events inside a logical operation.