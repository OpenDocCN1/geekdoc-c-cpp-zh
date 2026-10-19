and that can create a lot of problems. In C++ and similar languages, a variable can be visible to a block (a section of code enclosed in curly brackets), a routine, a class (and possibly its derived classes), or the whole program. In Java and C#, a variable can also be visible to a package or namespace (a collection of classes).

The following sections provide guidelines that apply to scope.

# Localize References to Variables

The code between references to a variable is a “window of vulnerability.” In the window, new code might be added, inadvertently altering the variable, or someone reading the code might forget the value the variable is supposed to contain. It’s always a good idea to localize references to variables by keeping them close together.

The idea of localizing references to a variable is pretty self-evident, but it’s an idea that lends itself to formal measurement. One method of measuring how close together the references to a variable are is to compute the “span” of a variable. Here’s an example:

```
Java Example of Variable Span
 a = 0;
 b = 0;
 c = 0;
 a = b + c;
```

In this case, two lines come between the first reference to a and the second, so a has a span of two. One line comes between the two references to b, so b has a span of one, and c has a span of zero. Here’s another example:

```
Java Example of Spans of One and Zero
 a = 0;
 b = 0;
 c = 0;
 b = a + 1;
 b = b / c;
```

Further Reading For more information on variable span, see Software Engineering Metrics and Models (Conte, Dunsmore, and Shen 1986).

In this case, there is one line between the first reference to b and the second, for a span of one. There are no lines between the second reference to b and the third, for a span of zero.

The average span is computed by averaging the individual spans. In the second example, for b, (1+0)/2 equals an average span of 0.5. When you keep references to variables close together, you enable the person reading your code to focus on one section at a time. If the references are far apart, you force the reader to jump around in the program. Thus the main advantage of keeping references to variables together is that it improves program readability.