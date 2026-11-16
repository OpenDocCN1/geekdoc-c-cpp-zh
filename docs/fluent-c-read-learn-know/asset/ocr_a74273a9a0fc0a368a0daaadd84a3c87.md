# # ENUMERATION SYNTAX

The syntax diagram below looks really confusing, doesn't it? And yet, you've seen that enumerations are simple to create and use. Like any statement that defines a type, enumerations must begin with the type keyword, which in this case is enum, followed by the name of the type, which must follow the rules for identifiers.

All of the members of the enumeration must be of the same numeric type. By default, that type is Int32, and most of the time that's fine because you don't usually care what the actual value is. But if for any reason you want to specify a different type, you do so by specifying the type name after the colon, as shown in the example.

After the identifier and the optional data type specification, you list the symbolic members of the type in braces, separated by commas. Again, since you won't usually care what the values of the member is because it's used symbolically, but if you do, you can specify the value using MemberName = Value in the list.

```
enum <Name> [: <type>] {<name> [=value], ...}
enum Ordinal : Int16 {First, Second, Fifth = 5};
```

> # MAKE A NOTE
> 
> It would be reasonable to think that if you build an enumeration and specify it as a parameter, you needn't worry about anybody passing an invalid argument. Unfortunately, there's a way around the restriction. We'll look at how to cast a value of one type to another type at the end of this chapter. Unlike enumerations, the syntax is simple, but the theory is a little complicated. Basically, to treat one type as an instance of another, you simply put the type name in parentheses in front of it:
> 
> (DaysOfTheWeek) 215 /
> 
> The .NET Framework lets you cast any Int32 to your Int32 enumeration, so that statement example will make it through the compiler just fine, despite the fact that the maximum value of the DaysOfTheWeek enumeration is 6. You'll still have to check for invalid arguments. Sigh.