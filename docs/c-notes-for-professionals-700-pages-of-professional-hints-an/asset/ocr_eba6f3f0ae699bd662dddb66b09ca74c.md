```
~~~csharp
Console.WriteLine(b is BaseInterface);  // True
Console.WriteLine(b is object);         // True
Console.WriteLine(b is string);         // False
~~~
```

If the intent of the cast is to use the object, it is best practice to use the as keyword'

```
~~~csharp
interface BaseInterface {}
class BaseClass : BaseInterface {}
class DerivedClass : BaseClass {}

var d = new DerivedClass();
Console.WriteLine(d is DerivedClass);   // True - valid use of 'is'
Console.WriteLine(d is BaseClass);      // True - valid use of 'is'

if(d is BaseClass){
    var castedD = (BaseClass)d;
    castedD.Method(); // valid, but not best practice
}

var asD = d as BaseClass;

if(asD!=null){
    asD.Method(); //preferred method since you incur only one unboxing penalty
}
~~~
```

But, from C# 7 pattern matching feature extends the is operator to check for a type and declare a new variable at the same time. Same code part with C# 7 :

```
~~~csharp
Version ≥ 7.0
if(d is BaseClass asD ){
    asD.Method();
}
~~~
```

# # Section 52.16: this

The **this** keyword refers to the current instance of class(object). That way two variables with the same name, one at the class-level (a field) and one being a parameter (or local variable) of a method, can be distinguished.

```
~~~csharp
public MyClass {
    int a;

    void set_a(int a)
    {
        //this.a refers to the variable defined outside of the method,
        //while a refers to the passed parameter.
        this.a = a;
    }
}
~~~
```

Other usages of the keyword are chaining non-static constructor overloads:

```
~~~csharp
public MyClass(int arg) : this(arg, null)
{
}
~~~
```

and writing indexers:

```
~~~csharp
public string this[int idx1, string idx2]
~~~
```