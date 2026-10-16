This code instantiates a delegate of type `GetAString` and initializes it so it refers to the `ToString` method of the integer variable x. Delegates in C# always syntactically take a one-parameter constructor, the parameter being the method to which the delegate refers. This method must match the signature with which you originally defined the delegate. In this case, you would get a compilation error if you tried to initialize the variable `firstStringMethod` with any method that did not take any parameters and return a string. Notice that because `int.ToString` is an instance method (as opposed to a static one), you need to specify the instance (x) as well as the name of the method to initialize the delegate properly.

The next line actually uses the delegate to display the string. In any code, supplying the name of a delegate instance, followed by parentheses containing any parameters, has exactly the same effect as calling the method wrapped by the delegate. Hence, in the preceding code snippet, the `Console.WriteLine` statement is completely equivalent to the commented-out line.

In fact, supplying parentheses to the delegate instance is the same as invoking the `Invoke` method of the delegate class. Because `firstStringMethod` is a variable of a delegate type, the C# compiler replaces `firstStringMethod` with `firstStringMethod.Invoke`:

```
firstStringMethod();
firstStringMethod.Invoke();
```

For less typing, at every place where a delegate instance is needed, you can just pass the name of the address. This is known by the term *delegate inference*. This C# feature works as long as the compiler can resolve the delegate instance to a specific type. The example initialized the variable `firstStringMethod` of type `GetAString` with a new instance of the delegate `GetAString`:

```
GetAString firstStringMethod = new GetAString(x.ToString);
```

You can write the same just by passing the method name with the variable x to the variable `firstStringMethod`:

```
GetAString firstStringMethod = x.ToString;
```

The code that is created by the C# compiler is the same. The compiler detects that a delegate type is required with `firstStringMethod`, so it creates an instance of the delegate type `GetAString` and passes the address of the method with the object x to the constructor.

> **NOTE** Be aware that you can’t type the brackets to the method name as `x.ToString()` and pass it to the delegate variable. This would be an invocation of the method. The invocation of the `ToString` method returns a string object that can’t be assigned to the delegate variable. You can only assign the address of a method to the delegate variable.