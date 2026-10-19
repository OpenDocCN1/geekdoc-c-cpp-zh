```
// public routines
FullName GetName() const;
String GetAddress() const;
String GetWorkPhone() const;
String GetHomePhone() const;
TaxId GetTaxIdNumber() const;
JobClassification GetJobClassification() const;
...
private:
...;
}
```

Internally, this class might have additional routines and data to support these services, but users of the class don’t need to know anything about them. The class interface abstraction is great because every routine in the interface is working toward a consistent end.

A class that presents a poor abstraction would be one that contained a collection of miscellaneous functions. Here’s an example:

![](bbox=[0.12, 0.42, 0.2, 0.52])

```
C++ Example of a Class Interface That Presents a Poor Abstraction
class Program {
public:
...
// public routines
void InitializeCommandStack();
void PushCommand( Command command );
Command PopCommand();
void ShutdownCommandStack();
void InitializeReportFormatting();
void FormatReport( Report report );
void PrintReport( Report report );
void InitializeGlobalData();
void ShutdownGlobalData();
...
private:
...;
}
```

Suppose that a class contains routines to work with a command stack, to format reports, to print reports, and to initialize global data. It’s hard to see any connection among the command stack and report routines or the global data. The class interface doesn’t present a consistent abstraction, so the class has poor cohesion. The routines should be reorganized into more-focused classes, each of which provides a better abstraction in its interface.

If these routines were part of a Program class, they could be revised to present a consistent abstraction, like so: