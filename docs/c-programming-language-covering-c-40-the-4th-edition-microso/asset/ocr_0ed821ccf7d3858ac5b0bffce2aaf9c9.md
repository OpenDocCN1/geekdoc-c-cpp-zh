When no dynamic expressions are involved, C# defaults to static binding, which means that the compile-time types of constituent expressions are used in the selection process. However, when one of the constituent expressions in the operations listed above is a dynamic expression, the operation is instead dynamically bound.

# ### 7.2.1 Binding Time

Static binding takes place at compile time, whereas dynamic binding takes place at runtime. In the following sections, the term *binding time* refers to either compile time or runtime, depending on when the binding takes place.

The following example illustrates the notions of static and dynamic binding and of binding time:

```
```
object o = 5;
dynamic d = 5;

Console.WriteLine(5); // Static binding to Console.WriteLine(int)
Console.WriteLine(o); // Static binding to Console.WriteLine(object)
Console.WriteLine(d); // Dynamic binding to Console.WriteLine(int)
```
```

The first two calls are statically bound: The overload of `Console.WriteLine` is picked based on the compile-time type of their argument. Thus the binding time is *compile time*.

The third call is dynamically bound: The overload of `Console.WriteLine` is picked based on the runtime type of its argument. This happens because the argument is a dynamic expression—its compile-time type is `dynamic`. Thus the binding time for the third call is *runtime*.

> **BILL WAGNER**  Many people confuse dynamic binding with type inference. Type inference is statically bound. The compiler determines the type at compile time. For example:
> 
> ```
> var i = 5;          // i is an int (Compiler performs type inference)
> Console.WriteLine(i); // Static binding to Console.WriteLine(int)
> ```
> 
> The compiler infers that `i` is an integer. All binding on the variable `i` uses static binding.

# ### 7.2.2 Dynamic Binding

The purpose of dynamic binding is to allow C# programs to interact with *dynamic objects*—that is, objects that do not follow the normal rules of the C# type system. Dynamic objects may be objects from other programming languages with different type systems, or they may be objects that are programmatically set up to implement their own binding semantics for different operations.