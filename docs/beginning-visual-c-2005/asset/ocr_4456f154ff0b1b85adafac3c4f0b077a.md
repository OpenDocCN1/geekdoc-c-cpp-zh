# Chapter 9

You could create a Handler delegate like this:

```
Handler^ handler = gcnew Handler(HandlerClass::Fun1);    // Delegate object
```

The handler object contains the address of the static function, Fun1, in the HandlerClass class. If you call the delegate, the HandlerClass::Fun1() function is called with the argument the same as you pass in the delegate call. You can write the delegate call like this:

```
handler->Invoke(90);
```

This calls all the functions in the invocation list for the handler delegate. In this case there is just one function in the invocation list, HandlerClass::Fun1(), so the output is:

```
Function1 called with value 90
```

You could also call the delegate with the following statement:

```
handler(90);
```

This is shorthand for the previous statement that explicitly called the Invoke() function and this is the form of delegate call you see generally.

The + operator is overloaded for delegate types to combine the invocation lists for two delegates into a new delegate object. For example, you could apparently modify the invocation list for the handler delegate with this statement:

```
handler += gcnew Handler(HandlerClass::Fun2);
```

The handler variable now references a delegate object with an invocation list containing two functions: Fun1 and Fun2. However, this is a new delegate object. The invocation list for a delegate cannot be changed so the + operator works in a similar way to the way it works with String objects(you always get a new object created. You could invoke the delegate again with this statement:

```
handler(80);
```

Now you get the output:

```
Function1 called with value 80
Function2 called with value 80
```

Both functions in the invocation list are called and they are called in the sequence in which they were added to the delegate object.

You can effectively remove an entry from the invocation list for a delegate by using the(operator:

```
handler -= gcnew Handler(HandlerClass::Fun1);
```

This creates a new delegate object that contains just HandlerClass::Fun2() in its invocation list because the effect is to remove the functions that are invocation list of the right side