Output 4.7 shows the results of Listing 4.14.

# OUTPUT 4.7

```
>ConvertToPhoneNumber.exe CSharpIsGood
274277474663
```

In this example, the TryGetPhoneButton() method returns true if it can successfully determine the character’s corresponding phone button. The function also returns the corresponding button by using the button parameter, which is decorated with out.

An out parameter is functionally identical to a ref parameter; the only difference is which requirements the language enforces regarding how the aliased variable is read from and written to. Whenever a parameter is marked with out, the compiler will check that the parameter is set for all code paths within the method that return normally (that is, the code paths that do not throw an exception). If, for example, the code does not assign button a value in some code path, the compiler will issue an error indicating that the code didn’t initialize button. Listing 4.14 assigns button to the underscore character because even though it cannot determine the correct phone button, it is still necessary to assign a value.

The developer of a method may declare one or more out parameters to get around the restriction that a method may have only one return type; a method that needs to return two values can do so by returning one value normally, as the return value of the method, and a second value by writing it into an aliased variable passed as an out parameter. Although this pattern is both common and legal, there are usually better ways to achieve that aim. For example, if you are considering returning two or more values from a method, you might actually be better off writing two methods, one for each value. If the method must return two values, use of tuple types (to represent multiple values) or nullable value types (to represent a value that might not be “valid,” as in the earlier example) can eliminate the need to pass variables by reference.

> NOTE
> Each and every normal code path must result in the assignment of all out parameters.