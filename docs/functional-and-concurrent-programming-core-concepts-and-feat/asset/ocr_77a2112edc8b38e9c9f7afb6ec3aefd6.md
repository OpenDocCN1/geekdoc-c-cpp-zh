# 9.6 Partial Application

Many Java interfaces can be implemented as lambdas, even though they predate Java's syntax for lambda expressions and have little to do with functional programming:

```
val absComp: Comparator[Int] = (x, y) => x.abs.compareTo(y.abs)
val stream: IntStream = ...
val loggingStream: IntStream = stream.onClose(() => logger.info("closing stream"))
```

Comparator is a Java 2 SAM interface with an abstract method compare. Stream method onClose uses a single argument of type Runnable, a Java 1 SAM interface with an abstract method run. Both Comparator and Runnable can be implemented as lambda expressions.

# 9.6 Partial Application

In addition to lambda expressions, currying, and η-conversion, partial application is yet another mechanism used to create function values. In Scala, it takes the form of an underscore used in place of a part of an expression. This produces a function that, when applied, replaces the underscore with its argument in the given expression. For instance, the following code searches for a temperature greater than 90 (in Fahrenheit) in a list of Celsius temperatures:

```
celsiusTemps.find(temp => temp * 1.8 + 32 > 90)
```

Instead of a lambda expression, you can build the desired function argument by replacing temp with an underscore in the expression temp * 1.8 + 32 > 90:

```
celsiusTemps.find(_ * 1.8 + 32 > 90)
```

The expression _ * 1.8 + 32 > 90 represents a Boolean function that maps temp to temp * 1.8 + 32 > 90, just like the function defined by the lambda expression temp => temp * 1.8 + 32 > 90. Searches written earlier using lambda expressions can use partial application instead:

```
temps.find(_ > 90)
projects.find(_ .id == 12345L)
```

Partial application is generalized to multi-argument functions by using several underscores in the same expression. For instance, _ * 1.8 + 32 > _ is a two-argument