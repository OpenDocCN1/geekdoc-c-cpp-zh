# F# code using an option

```
// return a string option to indicate the return value can be an uninitialized value
let str = read_string()
match str with
  Some data -> printf("good, we got value and we can process..."
  None -> printf("what happened, call IT right now!")
```

> > Note A simple implementation of read_string() is Console.ReadLine(). When Ctrl+Z is the console, Console.ReadLine() method returns NULL.

For the F# programmer, the situation is different. The user can give invalid input, so the code must represent the invalid input. An option type is used to explicitly indicate the invalid state. When an F# programmer invokes the read_string function, the returned option type reminds (or even forces) the F# programmer to handle this invalid situation. The design of F# helps the developer avoid many bugs. One typical example is how F# introduces an option other than using a NULL value to represent multiple types. If you count many NULL exceptions you received in the last month, it is not difficult to understand why F# programmers report bugs in their code.

Let's look at a customized class sample in C#. If you have a Person type object, what is the meaning of an assigned value NULL? It either the object is in an unassigned state or the object is in a special-case state (that is, it has an invalid value). This ambiguity breaks the single-responsibility principle, the first principle in SOLID. If two developers on the same team have a different view about what NULL means for the object, there will likely be many null-reference flaws in the application. If you compare this to the F# option approach, None is used to represent no value and Some(...) is used to represent any valid value. This clarifies the definition.

When we designed the language, we knew that not everyone agreed with the proceeding argument. This is totally fine because you use the AllowNullable attribute to make a class nullable. Listing 6-13 shows an example of how to use the AllowNullLiteral attribute.

+   LISTING 6-13 Using AllowNullLiteral on a type

```
<AllowNullable()>
type NullableType()
  member this.TestNullable(condition) =
    if condition then Nullable()
    else null
```