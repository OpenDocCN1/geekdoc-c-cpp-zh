To conclude, let's talk a bit about exceptions raised by one of the target methods for a multi-cast delegate. If one of the target methods throws an exception, that exception will bubble up through the delegate invocation call. This is nothing special, it seems, as long as you realize that this causes the target methods following the one that blew up not to execute:

```
Action good = () => { Console.WriteLine("OK"); };
Action boom = () => { throw new Exception("Boom!"); };
Action never = () => { Console.WriteLine("Never printed"); };

Action all = good + boom + never;
all(); // Prints OK and throws an exception, without reaching a call to "never"
```

If, for some obscure reason, you need to reliably invoke all target methods in the face of errors, you can do so by manual iteration over the invocation list. Doing so, you never swallow all exceptions and only deal with error conditions you can deal with appropriately:

```
foreach (Action target in all.GetInvocationList()) {
    try {
        target();
    }
    catch (SomeException ex) {
        // Handle SomeException appropriately
    }
}
```

# FOREACH'S HIDDEN CAST

In the preceding fragment, we're using a handy feature of the foreach statement that goes all the way back to C# 1.0 when generics weren't invented yet. Assume you're given some nongeneric collection (or a weakly typed array) and you happen to know it contains only strings. To give users easy iteration over the collection, C#'s foreach loop automatically inserted a cast from the retrieved object to the type specified on the loop variable:

```
object[] names = new string[] { "Bart", "John" };
foreach (string name in names) {
    // In reality, the enumerator's Current property returned an object,
    // so the compiler did emit code like:
    //     string name = (string)enumeratorOverNames.Current;
}
```

We're making handy use of this feature in the preceding code, as GetInvocationList returns a Delegate[], but we know the more specific type of each element in that array because add was obtained by combining Action delegates. By making Action the type for the target loop variable, we instruct the foreach loop to insert the cast on our behalf. Handy!