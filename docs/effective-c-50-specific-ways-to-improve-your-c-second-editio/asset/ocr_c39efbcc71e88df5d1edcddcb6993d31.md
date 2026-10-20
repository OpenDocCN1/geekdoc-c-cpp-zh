```
// Work with the circle.
// ...
```

```
// Convert to an ellipse.
Ellipse e = new Ellipse(c);
Flatten(e);
```

The variable e holds the flattened ellipse. By replacing the conversion operator with a constructor, you have not lost any functionality; you’ve merely made it clearer when new objects are created. (Veteran C++ programmers should note that C# does not call constructors for implicit or explicit conversions. You create new objects only when you explicitly use the new operator, and at no other time. There is no need for the explicit keyword on constructors in C#.)

Conversion operators that return fields inside your objects will not exhibit this behavior. They have other problems. You’ve poked a serious hole in the encapsulation of your class. By casting your type to some other object, clients of your class can access an internal variable. That’s best avoided for all the reasons discussed in Item 26.

Conversion operators introduce a form of substitutability that causes problems in your code. You’re indicating that, in all cases, users can reasonably expect that another class can be used in place of the one you created. When this substituted object is accessed, you cause clients to work with temporary objects or internal fields in place of the class you created. You then modify temporary objects and discard the results. These subtle bugs are hard to find because the compiler generates code to convert these objects. Avoid conversion operators in your APIs.

# Item 10: Use Optional Parameters to Minimize Method Overloads

C# now has support for named parameters at the call site. That means the names of formal parameters are now part of the public interface for your type. Changing the name of a public parameter could break calling code. That means you should avoid using named parameters in many situations, and also you should avoid changing the names of the formal parameters on public, or protected methods.

Of course, no language designer adds features just to make your life difficult. Named parameters were added for a reason, and they have positive