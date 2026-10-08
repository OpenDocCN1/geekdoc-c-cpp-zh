```
myClass.MyMethod(firstPar: 1, secondPar: "Hello");

// --- Most specific context: ChildClass
var childClass = new ChildClass();
childClass.MyMethod(firstArg: 1, secondArg: "Hello");
```

When the myClass variable is initialized, the compiler infers its type as BaseClass. So, both MyMethod calls use the parameter names in the most specific override that can be found by BaseClass. The childClass variable is a type of ChildClass, so when calling MyMethod through childClass, the context for parameter name resolution is ChildClass.

# Resolving Applicable Signatures

When you have a method with more than one overload, the compiler must resolve it during the build process. The compiler first filters the overloads to which are applicable to the method call context. If there are more candidates, the compiler uses "betterness" rules to select the best one.

With named and optional arguments, this process changed a bit from C# 3.0 to C# 4.0.

+   - A signature is applicable if all its parameters are optional, or have exactly one corresponding argument (by name or position) that is convertible to the parameter type.
- "Betterness" rules are only applied for arguments that are explicitly given — omitted arguments are ignored for betterness purposes.
- If two signatures are equally good (by terms of "betterness"), one that does not omit optional parameters is preferred.

Here is a short sample to demonstrate the resolution steps. MyClass defines four overloads for MyMethod:

```
public class MyClass {
    MyMethod(string s, int i = 1) { ... }
    MyMethod(object o) { ... }
    MyMethod(int i, string s = "C#") { ... }
    MyMethod(int i) { ... }
}
```

The question is which method should be called in the following code snippet?

```
var myClass = new MyClass();
myClass.MyMethod(2010);
```

Now, you can see how the rules work. MyMethod(string, int) is not applicable, because 2010 doesn't convert to string. MyMethod(int, string) is applicable because its second parameter is optional, and 2010 matches with its first argument. Obviously, MyMethod(object) and MyMethod(int) are also applicable.

Because there are three candidates, the "betterness" rules are applied. MyMethod(int, string) and MyMethod(int) are both better than MyMethod(object) because the conversion from 2010 to int is better than the conversion from 2010 to object.