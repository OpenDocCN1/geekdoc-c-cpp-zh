+   - The C# compiler looks only for extension methods defined in static classes that are themselves defined at the file scope. In other words, if you define the static class nested within another class, the C# compiler will emit the following message: error CS1109: Extension method must be defined in a top-level static class; StringBuilderExtensions is a nested class.

+   - Because the static classes can have any name you want, it takes the C# compiler time to find extension methods because it must look at all the file-scope static classes and scan their static methods for a match. To improve performance and also to avoid considering an extension method that you may not want, the C# compiler requires that you "import" extension methods. For example, if someone has defined a StringBuilderExtensions class in a WinTellect namespace, then a programmer who wants to have access to this class's extension methods must put a `using WinTellect;` directive at the top of his or her source code file.

+   - It is possible that multiple static classes could define the same extension method. If the compiler detects that two or more extension methods exist, then the compiler issues the following message: error CS0121: The call is ambiguous between the following methods or properties: 'StringBuilderExtensions.Index0f(string, char)' and 'AnotherStringBuilderExtensions.Index0f(string, char)'. To fix this error, you must modify your source code. Specifically, you cannot use the instance method syntax to call this static method anymore; instead you must now use the static method syntax where you explicitly indicate the name of the static class to explicitly tell the compiler which method you want to invoke.

+   - You should use this feature sparingly, because not all programmers are familiar with it. For example, when you extend a type with an extension method, you are actually extending derived types with this method as well. Therefore, you should not define an extension method whose first parameter is System.Object, because this method will be callable for all expression types and this will really pollute Visual Studio's IntelliSense window.

+   - There is a potential versioning problem that exists with extension methods. If, in the future, Microsoft adds an IndexOf instance method to their StringBuilder class with the same prototype as my code is attempting to call, then when I recompile my code, the compiler will bind to Microsoft's IndexOf instance method instead of my static IndexOf method. Because of this, my program will experience different behavior. This versioning problem is another reason why this feature should be used sparingly.

# ## Extending Various Types with Extension Methods

In this chapter, I demonstrated how to define an extension method for a class, StringBuilder. I'd like to point out that because an extension method is really the invocation of a static method, the CLR does not emit code ensuring that the value of the expression used to invoke the method is not null.

```
```csharp
// sb is null
StringBuilder sb = null;
```
```