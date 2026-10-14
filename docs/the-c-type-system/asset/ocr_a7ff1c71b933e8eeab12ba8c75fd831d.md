```
{
    if(item.Time.Date == time.Date)
        yield return item;
}
```

Listing 3-16: A ref parameter in an iterator

Here the AppointmentsForDay method is attempting to filter the items sequence passed as a parameter for elements that match the time parameter. However, like closures, methods that use iterator blocks can’t have by-reference parameters, so the method in Listing 3-16 fails to compile, with this error:

```
[CS1623] Iterators cannot have ref, in or out parameters
```

Each time the method yields a value, control returns to the calling code. When the next item is requested, the method must continue at the statement following the yield and must do so with the same state. The compiler transforms the yield statement to return an instance of the iterator block class that captures the state between requests for each element, similar to the way closures work.

The compiler-generated class needs to capture all the method parameters and any local variables as fields to preserve the method’s state between each request for a value, which is why iterator methods can’t have by-reference parameters.

# Asynchronous Methods

Lastly, and for exactly the same reason as closures and iterator blocks, we can’t declare by-reference parameters for async methods like the TryGetResponse method in Listing 3-17.

```
public static async Task<bool> TryGetResponse(out string response)
{
    response = await Task.Run(() => GetUserInput());
    return !string.IsNullOrEmpty(response);
}
```

Listing 3-17: An out parameter in an asynchronous method

This method fails to compile with the following error:

```
[CS1988] Async methods cannot have ref, in or out parameters
```

In this instance, the compiler synthesizes a hidden class to manage the asynchronous invocation of the Task.Run method. Asynchronous methods return control to their caller when the await statement is reached, and so, like iterator blocks, they must preserve the state of all their variables. The compiler-generated class captures all local variables and parameters as