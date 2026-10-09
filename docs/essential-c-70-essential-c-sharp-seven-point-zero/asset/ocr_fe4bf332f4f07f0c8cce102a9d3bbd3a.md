infers the type from the location of the call. If the compiler can make no such inference, the name must be provided as part of the method call.

At their core, types are a means of grouping together methods and their associated data. For example, Console is the type that contains the Write(), WriteLine(), and ReadLine() methods (among others). All of these methods are in the same group because they belong to the Console type.

# Scope

In the previous chapter, you learned that the scope of a program element is the region of text in which it can be referred to by its unqualified name. A call that appears inside a type declaration to a method declared in that type does not require the type qualifier because the method is in scope throughout its containing type. Similarly, a type is in scope throughout the namespace that declares it; therefore, a method call that appears in a type in a particular namespace need not specify that namespace in the method call name.

# Method Name

Every method call contains a method name, which might or might not be qualified with a namespace and type name, as we have discussed. After the method name comes the argument list; the argument list is a parenthesized, comma-separated list of the values that correspond to the parameters of the method.

# Parameters and Arguments

A method can take any number of parameters, and each parameter is of a specific data type. The values that the caller supplies for parameters are called the arguments; every argument must correspond to a particular parameter. For example, the following method call has three arguments:

```
System.IO.File.Copy(  
    oldFileName, newFileName, false)
```

The method is found on the class File, which is located in the namespace System.IO. It is declared to have three parameters, with the first and second being of type string and the third being of type bool. In this example, we use variables (oldFileName and newFileName) of type string for the old and new filenames, and then specify false to indicate that the copy should fail if the new filename already exists.