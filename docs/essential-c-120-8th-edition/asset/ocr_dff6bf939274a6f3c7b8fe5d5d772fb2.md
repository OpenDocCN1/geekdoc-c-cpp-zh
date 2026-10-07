listing handles three property types: Boolean, string, and enum. In the case of enums, you parse the option value and assign the text's enum to the property. Assuming the TryParse() call was successful, the method exits and the CommandLineInfo object is initialized with the data from the command line.

Interestingly, although CommandLine private class nested within Program, CommandLineHandler has no trouble reflecting over it and invoking its members. In other words, reflection can circumvent accessibility rules as long as appropriate permissions are established. For example, if Out was private, the TryParse() method could still assign a value. Because of this, it would be possible to move CommandLineHandler into a separate assembly and share it across multiple programs, each with its own CommandLineInfo class.

In this example, you invoke a member on CommandLineInfo using PropertyInfo.SetValue(). Not surprisingly, PropertyInfo also includes a GetValue() method for retrieving data from the property. For a method, however, there is a MethodInfo with an Invoke() member. Both MethodInfo and PropertyInfo derive from MemberInfo (albeit indirectly), as shown in Figure 18.1.

# Reflection on Generic Types

The introduction of generic types in version 2.0 of the Common Language Runtime (CLR) necessitated additional reflection features. Runtime reflection on generics determines whether a class or method contains a generic type and any type parameters or arguments it may include.

# Determining the Type of Type Parameters

In the same way that you can use a typeof operator on nongeneric types to retrieve an instance of System.Type, so you can use the typeof operator on type parameters in a generic type or generic method. Listing 18.4 applies the typeof operator to the type parameter in the Add method of a Stack class.

LISTING 18.4: Declaring the Stack<T> Class

```
public class Stack<T>
{
    //...
```