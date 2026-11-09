# ## Chapter 10

# # Properties

+   **In this chapter:**
+   
+   - Parameterless Properties .......... 237
+   - Parameterful Properties .......... 252
+   - The Performance of Calling Property Accessor Methods .......... 257
+   - Property Accessor Accessibility .......... 258
+   - Generic Property Accessor Methods .......... 258

In this chapter, I’ll talk about properties. Properties allow source code to call a method by using a simplified syntax. The common language runtime (CLR) offers two kinds of properties: parameterless properties, which are simply called *properties*, and parameterful properties, which are called different names by different programming languages. For example, C# calls parameterful properties *indexers*, and Microsoft Visual Basic calls them *default properties*. I’ll also talk about initializing properties using object and collection initializers as well as ways to package a bunch of properties together using C#’s anonymous types and the `System.Tuple` type.

# ## Parameterless Properties

Many types define state information that can be retrieved or altered. Frequently, this state information is implemented as field members of the type. For example, here’s a type definition that contains two fields:

```
```
public sealed class Employee {
    public String Name;   // The employee's name
    public Int32  Age;    // The employee's age
}
```
```

If you were to create an instance of this type, you could easily get or set any of this state information with code similar to the following:

```
```
Employee e = new Employee();
e.Name = "Jeffrey Richter";   // Set the employee's Name.
e.Age  = 45;                  // Set the employee's Age.

Console.WriteLine(e.Name);    // Displays "Jeffrey Richter"
```
```

Querying and setting an object’s state information in the way I just demonstrated is very common. However, I would argue that the preceding code should never be implemented as