```
Fraction *f1;
```

Which do you think is more understandable—that is, which makes the intended use of the variable f1 clearer? The combination of static typing and meaningful variable names (which we intentionally did not choose in the previous example) can go a long way toward making your program self-documenting.

# Argument and Return Types with Dynamic Typing

If you use dynamic typing to invoke a method, note the following rule: If a method with the same name is implemented in more than one of your classes, each method must agree on the type of each argument and the type of value it returns so that the compiler can generate the correct code for your message expressions.

The compiler performs a consistency check among each class declaration it has seen. If one or more methods conflict in either argument or return type, the compiler issues a warning message. For example, both the Fraction and Complex classes contain add: methods. However, the Fraction class takes as its argument and returns a Fraction object, whereas the Complex class takes returns a Complex object. if frac1 and myFract are Fraction objects, compl and myComplex are Complex objects, statements such as

```
result = [myFract add: frac1];
```

and

```
result = [myComplex add: compl];
```

do not cause any problems. This is because, in both cases, the receiver of the message is statically typed and the compiler can check for consistent use of the method as it is defined in the receiver's class.