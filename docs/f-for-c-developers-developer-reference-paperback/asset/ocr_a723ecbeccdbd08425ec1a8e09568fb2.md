# LISTING 2-2 A class definition

```
Class definition without a default accessibility modifier
// define a public Point2D class
type Point2D() = class

end
```

```
Class definition with an explicit accessibility modifier
// define an internal Point2D class
type internal Point2D() = class

end

// define a class without the class keyword
type MyClass() =
// class fields, methods, and properties, such as the following field
let myField = 9
```

> Note If the class does not contain any member or operation, you have to use class keyword; otherwise, class keyword is optional.

You might be wondering where the public keyword is. Unlike class in C#, which is internal by default, the F# class is public by default. Ignoring the public keyword can save some typing. F# also supports supports using modules to group code. Table 2-1 lists all of the accessibility modifiers that F# supports.

# TABLE 2-1 Accessibility modifier definitions

| Accessibility Modifier | Description |
|---|---|n| public | The public access indicates that the type, value, and function are accessible anywhere. |
| private | The private access modifier is the least-permissive access. Private members are accessible within the body of the class or the struct in which they are declared. The class field is private by default. |
| internal | The internal modifier is same as public if there is only one assembly. The internal types are not accessible from another assembly. It is public when accessed from the same assembly and when access from a different assembly. |

> Note F# does not support the protected keyword. F# honors protected visibility when the type is defined in a language that supports protected-level visibility. F# intends to use less protected level members in a class than in C# instead, it uses interfaces, object expressions, and higher order functions.