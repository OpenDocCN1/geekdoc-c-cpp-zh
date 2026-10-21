```
```scala
temps.find(greaterThan(90))
temps.find(greaterThan(80))
```
```

In a similar fashion, you can define a function to generate search criteria for projects:

```
```scala
def hasID(identity: Long): Project => Boolean = 
def hasGivenID(project: Project): Boolean = project.id == identity
hasGivenID
projects.find(hasID(12345L))
projects.find(hasID(54321L))
```
```



Functions that return other functions are common in functional programming, and many languages define a more convenient syntax for them:

```
```scala
def greaterThan(bound: Int)(x: Int): Boolean = x > bound
def hasID(identity: Long)(project: Project): Boolean = project.id == identity
```
```

Listing 9.4 Example of higher-order functions defined through currying.

It might appear as if greaterThan is a function of two arguments, bound and x, but it is not. It is a function of a single argument, bound, which returns a function of type Int => Boolean, as before; x is actually an argument of the function being returned.

Functions written in this style are said to be curried.1 A curried function is a function that consumes its first list of arguments, returns another function that uses the next argument list, and so on. You can read the definition of greaterThan as implementing a function that takes an integer argument bound and returns another function, which takes an integer argument x and returns the Boolean x > bound. In other words, the return value of greaterThan is the function that maps x to x > bound.

Functional programming languages rely heavily on currying. In particular, currying can be used as a device to implement all functions as single-argument functions, as in

> 1The concept is named after the logician Haskell Curry, and the words curried and currying are sometimes capitalized.