![](bbox=[0.15, 0.12, 0.55, 0.3])

FIGURE 15.14 Default(T) relies on initobj to get its behavior.

# Getting the Type's Reflection Info Object

The other operation that's meaningfully defined on a generic parameter T is the typeof expression that gets the System.Type object describing, at runtime, the type that was supplied for the type parameter T:

```
Type t = typeof(T);
var methods = t.GetMethods();
```

Because you'll be reading a whole chapter about reflection (Chapter 21, “Reflection”), we defer further discussion about System.Type until later. Practically speaking, you should rarely have to use the typeof(T) trick.

# Generic Constraints

So far, you've learned how to declare a generic type and how to use it. Although the latter operation will be your main point of contact with the world of generics, you'll sometimes want to write your own generic type. However, up to this point, we haven't been able to do much with a generic type parameter inside the type definition. Let's take a look from an abstract point of view first. Consider the following piece of code:

```
class Foo<T> {
    public void Bar(T input) {
        // What can be do with T?
    }
}
```

The main question is what we can do with the input received as a parameter on Bar. For one thing, we can take the object and store it somewhere (for example, in a private field). That's precisely what a List<T> does, sticking the received elements in an array with element type T. For example: