Here, the first call to Console.WriteLine involves calling ToString on a variable that's statically typed to be Bar. The compiler will find a ToString method on the Bar type that hides the inherited member, so it chooses that one. As a result, the first call will print “Hi there!”

The second call, however, uses the WriteLine overload that accepts System.Object as its argument. Inside WriteLine, ToString will be invoked without any compile-time knowledge of the type passed in, other than the fact it is a System.Object. A virtual call results. Because we didn't override ToString but have hidden it, the default ToString method, inherited from System.Object, is called, hence printing Bar's type name.

If we were to do things polymorphically by assigning the newly created Bar instance to a variable of type System.Object, things are different, too:

```
object o = b;
Console.WriteLine(o.ToString());
Console.WriteLine(o);
```

Now, both calls to ToString, once explicitly and once by Console.WriteLine's code, result in a virtual call. Because Bar hasn't overridden the ToString method, both calls print the type name of Bar.

# How Virtual Dispatch Works

At first sight, virtual dispatch might look like a bit of magic. The compiler did know about a static type, yet a virtual method override on the runtime type is considered for execution. How does that work? The answer lies in the runtime facilities provided for method calls. A set of different instructions exist to call methods, two of which are used by the C# compiler. One is call, the other is callvirt. From the name, you can already infer the task of the second (although the C# compiler uses it for other purposes, as you will see).

Consider the following piece of code, given our Shape and Circle classes we defined earlier. Observe how the call to Radius involves a nonvirtual member, whereas the call to Area should be carried out using virtual dispatch.

```
Circle c = new Circle(3.0);
Console.WriteLine(c.Radius);

Shape s = c;
Console.WriteLine(s.Area);
```

Figure 14.14 shows the IL code corresponding to the preceding fragment. A few things should be pointed out. First, notice how all calls to the static WriteLine method overloads are carried out using the call instruction. Because static methods can never be virtual (after all, you call them by specifying a type name), this is expected. However, both calls for the Radius and Area property getters are done using callvirt. When looking at the code for Shape and Circle, you would expect only the get_Area call to use callvirt. The reason both use callvirt is a difference in behavior with regard to null checks: callvirt will properly throw a NullReferenceException as soon as it sees the target is a null reference.