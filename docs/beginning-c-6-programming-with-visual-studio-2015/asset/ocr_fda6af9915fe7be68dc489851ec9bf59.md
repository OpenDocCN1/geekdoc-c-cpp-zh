MyInternalClass, which is internally accessible. Note that this class was implicitly internal by default when you created it, as it had no access modifier. It is good practice to be explicit about accessibility, though, because it makes your code more readable, which is why you add the internal keyword. The console application project, Ch09Ex02, contains simple code that makes use of the class library project.

> NOTE When an application uses classes defined in an external library, you can call that application a client application of the library. Code that uses a class that you define is often similarly referred to as client code.

To use the classes in Ch09ClassLib, you added a reference to Ch09ClassLib.dll to the console application. For the purposes of this example, you simply point at the output file for the class library, although it would be just as easy to copy this file to a location local to Ch09Ex02, enabling you to continue development of the class library without affecting the console application. To replace the old assembly version with the new one, simply copy the newly generated DLL file over the old one.

After adding the reference, you took a look at the available classes using the Object Browser. Because the MyInternalClass is internal, you can't see it in this display — it isn't accessible to external projects. However, MyExternalClass is accessible, and it's the one you use in the console application.

You could replace the code in the console application with code attempting to use the internal class as follows:

```
static void Main(string[] args)
{
    MyInternalClass myObj = new MyInternalClass();
    WriteLine(myObj.ToString());
    ReadKey();
}
```

If you attempt to compile this code, you receive the following compilation error:

```
'Ch09ClassLib.MyInternalClass'
is inaccessible due to its protection level
```

This technique of making use of classes in external assemblies is key to programming with C# and the .NET Framework. It is, in fact, exactly what you are doing when you use any of the classes in the .NET Framework because they are treated in the same way.

# INTERFACES VERSUS ABSTRACT CLASSES

This chapter has demonstrated how you can create both interfaces and abstract classes (without members for now — you get to them in Chapter 10). The two types are similar in a number of ways, so it would be useful to know how to determine when you should use one technique or the other.

First the similarities: Both abstract classes and interfaces can contain members that can be inherited by a derived class. Neither interfaces nor abstract classes can be directly instantiated, but it is possible to declare variables of these types. If you do, you can use polymorphism to assign objects that