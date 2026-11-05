```
var myClass = new SomeClass<int>();
myClass.PrintTypeName();

Console.WriteLine(nameof(SomeClass<int>));
```

# Console Output

+   - TItem
+   - SomeClass

# Section 9.7: Printing a parameter name

# Snippet

```
public void DoSomething(int paramValue)
{
    Console.WriteLine(nameof(paramValue));
}

...

int myValue = 10;
DoSomething(myValue);
```

# Console Output

+   - paramValue

# Section 9.8: Applied to qualified identifiers

# Snippet

```
Console.WriteLine(nameof(CompanyNamespace.MyNamespace));
Console.WriteLine(nameof(MyClass));
Console.WriteLine(nameof(MyClass.MyNestedClass));
Console.WriteLine(nameof(MyNamespace.MyClass.MyNestedClass.MyStaticProperty));
```

# Console Output

+   - MyNamespace
+   - MyClass
+   - MyNestedClass
+   - MyStaticProperty