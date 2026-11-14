Now, what happens when you execute this code?

```
var obj2 = new D();
obj2.Foo(new D());
obj2.Foo(new B());
```

Both lines print “in D.Foo”. You always call the method in the derived class. Any number of developers would figure that the first call would print “in B.Foo”. However, even the simple overload rules can be surprising. The reason both calls resolve to D.Foo is that when there is a candidate method in the most derived compile-time type, that method is the better method. That’s still true when there is even a better match in a base class. Of course, this is very fragile. What do you suppose this does:

```
B obj3 = new D();
obj3.Foo(new D());
```

I chose the words above very carefully because obj3 has the compile-time type of B (your Base class), even though the runtime type is D (your Derived class). Foo isn’t virtual; therefore, obj3.Foo() must resolve to B.Foo.

If your poor users actually want to get the resolution rules they might expect, they need to use casts:

```
var obj4 = new D();
((B)obj4).Foo(new D());
obj4.Foo(new B());
```

If your API forces this kind of construct on your users, you’ve failed. You can easily add a bit more confusion. Add one method to your base class, B:

```
public class B
{
    public void Foo(D2 parm)
    {
        Console.WriteLine("In B.Foo");
    }

    public void Bar(B2 parm)
    {
        Console.WriteLine("In B.Bar");
    }
}
```