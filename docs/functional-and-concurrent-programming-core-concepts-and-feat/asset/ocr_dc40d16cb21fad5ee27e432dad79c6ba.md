In Scala, you can call a single-argument function on an expression delimited by curly braces without the need for additional parentheses. So, instead of writing

```
println({
  val two = 2
  two + two
}) // prints 4
```

you can simply write:

```
println {
  val two = 2
  two + two
} // prints 4
```

To use this syntax when multiple arguments are involved, you can rely on currying to adapt a multi-argument function into a single-argument function. For instance, the curried variant of function plus can be invoked as follows:

```
plus(5) {
  val two = 2
  two + 1
}
```

This is still value 8, as before.

Many functions and methods are curried in Scala for the sole purpose of benefiting from this syntax. The syntax is introduced here because we will encounter some example uses throughout the book, starting with the next section.

# 9.3 Function Literals

It would be inconvenient if, to use higher-order functions like find, you always had to separately define (and name) argument functions like hasID12345 and greaterThan90. After all, when you call a function on a string or an integer, you don’t need to define (and name) the values first. This is because programming languages define a syntax for strings and integer literals, like the "foo" and 42 that are sprinkled throughout this book’s code illustrations. Similarly, functional programming languages, which rely heavily on higher-order functions, offer syntax for function literals, also called anonymous functions. The most common form of function literals is lambda expressions, which are often the first