shouldn't be concerned about this inconsistency because non-CLS-compliant attributes are incredibly rare. In fact, in all of the time I've been working with the .NET Framework, I've never even seen one.

> **Note** Be aware that only Attribute, Type, and MethodInfo classes implement reflection methods that honor the Boolean inherit parameter. All other reflection methods that look up attributes ignore the inherit parameter and do not check the inheritance hierarchy. If you need to check the presence of an inherited attribute for events, properties, fields, constructors, or parameters, you must call one of Attribute's methods.

There's one more thing you should be aware of: When you pass a class to IsDefined, GetCustomAttribute, or GetCustomAttributes, these methods search for the application of the attribute class you specify or any attribute class derived from the specified class. If your code is looking for a specific attribute class, you should perform an additional check on the returned value to ensure that what these methods returned is the exact class you're looking for. You might also want to consider defining your attribute class to be sealed to reduce potential confusion and eliminate this extra check.

Here's some sample code that lists all of the methods defined within a type and displays the attributes applied to each method. The code is for demonstration purposes; normally, you wouldn't apply these particular custom attributes to these targets as I've done here.

```
```csharp
using System;
using System.Diagnostics;
using System.Reflection;


[assembly: CLSCompliant(true)]


[Serializable]
[DefaultMemberAttribute("Main")]
[DebuggerDisplayAttribute("Richter", Name = "Jeff", Target = typeof(Program))]
public sealed class Program {
    [Conditional("Debug")]
    [Conditional("Release")]
    public void DoSomething() { }

    public Program() {
    }

    [CLSCompliant(true)]
    [STAThread]
    public static void Main() {
        // Show the set of attributes applied to this type
        ShowAttributes(typeof(Program));
```
```