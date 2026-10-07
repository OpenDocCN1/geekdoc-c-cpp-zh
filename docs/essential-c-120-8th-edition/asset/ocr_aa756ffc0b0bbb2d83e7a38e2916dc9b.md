# Chapter 5: Parameters and Methods

```
// ...
}
```

(Note that a return statement transfers control out of the switch, so no break statement is required to prevent illegal fall-through in a switch section that ends with a return statement.)

In Listing 5.5, the last statement in the method is not a return statement; it is a switch statement. However, the compiler can deduce that every possible code path through the method results in a return, so that the end point of the method is not reachable. Thus, this method is legal even though it does not end with a return statement.

If particular code paths include unreachable statements following the return, the compiler will issue a warning that indicates the additional statements will never execute.

Though C# allows a method to have multiple return statements, code is generally more readable and easier to maintain if there is a single exit location rather than multiple returns sprinkled through various code paths of the method.

Specifying void as a return type indicates that there is no return value from the method. As a result, a call to the method may not be assigned to a variable or used as a parameter type at the call site. A void method may be called only as a statement. Furthermore, within the body of the method the return statement becomes optional, and when it is specified, there must be no value following the return keyword. For example, the return of Main() in Listing 5.4 is void, and there is no return statement in the method. However, DisplayGreeting() includes an (optional) return statement that is not followed by any returned result.

Although, technically, a method can have only one return type, the return type could be a tuple. As a result, starting with C# 7.0, it is possible to return multiple values packaged as a tuple using C# tuple syntax. For example, you could declare a GetName() method, as shown in Listing 5.6.

# Listing 5.6: Returning Multiple Values Using a Tuple

```
public class Program{
    static string GetUserInput(string prompt)
    {
```