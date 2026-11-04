![](bbox=[0.12, 0.11, 0.68, 0.47])

FIGURE 13.1 Pairwise operator declaration enforcement.

# The Role of System.Object's Instance Equals Method

Defined on System.Object, the "mother type of all types", the Equals instance method is used to compare whether two objects are "equal," whatever that means for the types of the target object and the one being compared.

```
class Object
{
    ...
    public virtual bool Equals(object obj) { /* default implementation */ }
}
```

As you learn in Chapter 14, "Object-Oriented Programming," virtual methods can be overridden by deriving types. It's typical for types to do so for System.Object's virtual methods, which include Equals, GetHashCode, and ToString. Before we get into overriding the Equals method, let's discuss its default behavior.

For reference types, the default Equals method implementation performs a reference equality, checking whether both references refer to the same object. For value types, a bitwise equality is carried out, checking whether both values carry the same data. This is illustrated in Figure 13.2, where public fields are used to keep things simple.

# WHAT ABOUT BOXING?

Because reference types get compared by reference equality and boxed value types are a form of reference types, you might wonder about the outcome of the following code (with Point declared as a struct).

```
var p1 = new Point { X = 3, Y = 5 };
var p2 = new Point { X = 3, Y = 5 };
Console.WriteLine(p1.Equals(p2));
```