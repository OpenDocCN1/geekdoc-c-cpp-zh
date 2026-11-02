# Statements and expressions

Any part of a computer program that has a value is called an expression. If you write `gumballs = 30;` then 30 is an expression (an expression whose value is the quantity 30). If you write `amount = 5.95 + 25.00;` then 5.95 + 25.00 is an expression (because 5.95 + 25.00 has the value 30.95). If you write `gumballsPerKid = gumballs / kids;` then `gumballs / kids` is an expression. (The value of the expression `gumballs / kids` depends on whatever values the variables `gumballs` and `kids` have when the expression with the expression in it is executed.)

This brings us to the subject of the pre- and postincrement and decrement operators. There are two ways to think about these operators: the way everyone understands it and the right way. The way I explain it in most of this section (in terms of time, with before and after) is the way everyone understands the concept. Unfortunately, the way everyone understands the concept isn't really the right way. When you see ++ or --, you can think in terms of time sequence. But occasionally some programmer uses ++ or -- in a convoluted way, and the notions of before and after break down. So if you're ever in a tight spot, you should think about these operators in terms of statements and expressions.

First, remember that a statement tells the computer to do something, and an expression has a value. (Statements are described in Chapter 4, and expressions are described earlier in this sidebar.) Which category does `gumballs++` belong to? The surprising answer is both. The Java code `gumballs++` is both a statement and an expression.

Suppose that, before executing the code `System.out.println(gumballs++)`, the value of `gumballs` is 28:

+   - As a statement, `gumballs++` tells the computer to add 1 to gumballs.
+   - As an expression, the value of `gumballs++` is 28, not 29.

So even though `gumballs` gets 1 added to it, the code `System.out.println(gumballs++)` really means `System.out.println(28)`. (See the figure in this sidebar.)

Now, almost everything you just read about `gumballs++` is true about `++gumballs`. The only difference is, as an expression, `++gumballs` behaves in a more intuitive way. Suppose that before executing the code `System.out.println(++gumballs)`, the value of `gumballs` is 28:

+   - As a statement, `++gumballs` tells the computer to add 1 to gumballs.
+   - As an expression, the value of `++gumballs` is 29.

So with `System.out.println(++gumballs)`, the variable `gumballs` gets 1 added to it, and the code `System.out.println(++gumballs)` really means `System.out.println(29)`.