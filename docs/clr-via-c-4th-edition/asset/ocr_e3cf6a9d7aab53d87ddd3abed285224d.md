The following code shows how to use reflection to call a method ("Contains") on a String target ("Jeffrey Richter") passing it a String argument ("ff") and storing the Boolean result in a local variable (result).

```
~~~csharp
Object target = "Jeffrey Richter";
Object arg = "ff";

// Find a method on the target that matches the desired argument types
Type[] argTypes = new Type[] { arg.GetType() };
MethodInfo method = target.GetType().GetMethod("Contains", argTypes);

// Invoke the method on the target passing the desired arguments
Object[] arguments = new Object[] { arg };
Boolean result = Convert.ToBoolean(method.Invoke(target, arguments));
~~~
```

Using C#'s dynamic type, this code can be rewritten with greatly improved syntax.

```
~~~csharp
dynamic target = "Jeffrey Richter";
dynamic arg = "ff";
Boolean result = target.Contains(arg);
~~~
```

Earlier, I mentioned that the C# compiler emits payload code that, at run time, figures out what operation to perform based on the actual type of an object. This payload code uses a class known as a runtime binder. Different programming languages define their own runtime binders that encapsulate the rules of that language. The code for the C# runtime binder is in the Microsoft.CSharp.dll assembly, and you must reference this assembly when you build projects that use the dynamic keyword. This assembly is referenced in the compiler's default response file, CSC.rsp. It is the code in this assembly that knows how to produce code (at run time) that performs addition when the + operator is applied to two Int32 objects and concatenation when applied to two String objects.

At run time, the Microsoft.CSharp.dll assembly will have to load into the AppDomain, which hurts your application's performance and increases memory consumption. Microsoft.CSharp.dll also loads System.dll and System.Core.dll. If you are using dynamic to help you interoperate with COM components, then System.Dynamic.dll will also load. And when the payload code executes, it generates dynamic code at run time; this code will be in an in-memory assembly called "Anonymously Hosted DynamicMethods Assembly." The purpose of this code is to improve the performance of dynamic dispatch in scenarios where a particular call site is making many invocations using dynamic arguments that have the same runtime type.

Due to all the overhead associated with C#'s built-in dynamic evaluation feature, you should consciously decide that you are getting sufficient syntax simplification from the dynamic feature to make it worth the extra performance hit of loading all these assemblies and the extra memory that they consume. If you have only a couple places in your program where you need dynamic behavior, it might be more efficient to just do it the old-fashioned way, by calling reflection methods (for managed objects) or with manual casting (for COM objects).

At run time, the C# runtime binder resolves a dynamic operation according to the runtime type of the object. The binder first checks to see if the type implements the IDynamicMetaObjectProvider interface. If the object does implement this interface, then the interface's GetMetaObject method is