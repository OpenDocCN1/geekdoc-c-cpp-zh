```
var verbosity = 0
if arg == "-v" then verbosity = 1
else if arg == "-vv" then verbosity = 2
```

This sets verbosity to the desired value, but the variable is reassignable, and there is no referential transparency. Could verbosity be declared as a val instead? A programmer used to a more functional style would implement the calculation in this way:

```
val verbosity = if arg == "-v" then 1 else if arg == "-vv" then 2 else 0
```

The trick is to use if-then-else functionally, as an expression, and then to set verbosity to the value of that expression, once and for all.

If your experience has been mostly with imperative programming, you may find the first version easier to understand. It does take a little time to get used to thinking in terms of expressions instead of statements. As a trend, however, many programming languages offer improved support for programming with expressions. Java, for instance, retrofitted its switch statement in version 14 to become an expression. You could use it to implement the parsing example:

```
final int verbosity = switch (arg) {
  case "-v" -> 1;
  case "-vv" -> 2;
  default -> 0;
};
```

In Java, final is used to prevent variable reassignment. If you use the earlier imperative approach to define verbosity, you won’t be able to mark it as final.

# 3.5 Immutable Objects

Declaring a variable using val guarantees that the name continues to refer to the same value while in scope. However, if this value is a mutable object, the object itself might still change (as in Listing 2.6, for instance). To get the full power of referential transparency, you need to use val to refer to immutable values.

An object is immutable, also called functional or persistent, if its own state cannot be changed. Many common Java types, such as String and BigInteger, define immutable objects. You are probably already familiar with the benefits of using immutable objects, such as for avoiding aliasing issues or facilitating inter-thread sharing. A functional programming style emphasizes their use even more, a pattern sometimes known as functional-object-oriented programming.

Like defining val variables or thinking of if-then-else as an expression, using and designing immutable objects may require some adjustment if you come from an