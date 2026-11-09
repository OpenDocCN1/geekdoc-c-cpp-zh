Recall that System.Object defines a public, nonvirtual instance method named GetType. When you call this method, the CLR determines the specified object's type and returns a reference to its Type object. Because there is only one Type object per type in an AppDomain, you can use equality and inequality operators to see whether two objects are of the same type.

```
    private static Boolean AreObjectsTheSameType(object o1, object o2) {
        return o1.GetType() == o2.GetType();
    }
```

In addition to calling Object's GetType method, the FCL offers several more ways to obtain a Type object:

+   - The System.Type type offers several overloaded versions of the static GetType method. All versions of this method take a String. The string must specify the full name of the type (including its namespace). Note that the primitive type names supported by the compiler (such as C#'s int, string, bool, and so on) aren't allowed because these names mean nothing to the CLR. If the string is simply the name of a type, the method checks the calling assembly to see whether it defines a type of the specified name. If it does, a reference to the appropriate Type object is returned.

If the calling assembly doesn't define the specified type, the types defined by MSCorLib.dll are checked. If a type with a matching name still can't be found, null is returned or a System.TypeLoadException is thrown, depending on which overload of the GetType method you called and what parameters you passed to it. The FCL documentation fully explains this method.

You can pass an assembly-qualified type string, such as "System.Int32, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089", to GetType. In this case, GetType will look for the type in the specified assembly (loading the assembly if necessary).

+   - The System.Type type offers a static ReflectionOnlyGetType method. This method behaves similarly to the GetType method mentioned in the previous bullet, except that the type is loaded so that it can be reflected over but cannot be executed.

+   - The System.TypeInfo type offers the following instance members: DeclaredNestedTypes and GetDeclaredNestedType.

+   - The System.Reflection.Assembly type offers the following instance members: GetType, DefinedTypes, and ExportedTypes.

**Note** Microsoft has defined a Backus-Naur Form grammar for type names and assembly-qualified type names that is used for constructing strings that will be passed to reflection methods. Knowledge of the grammar can come in quite handy when you are using reflection, specifically if you are working with nested types, generic types, generic methods, reference parameters, or arrays. For the complete grammar, see the FCL documentation or do a web search for "Backus-Naur Form Grammar for Type"