languages like Haskell and ML. For instance, we tend to think of addition as a function of two arguments:

```
def plus(x: Int, y: Int): Int = x + y // a function of type (Int, Int) => Int
plus(5, 3) // 8
```

However, you can also think of it as a single-argument (higher-order) function:

```
def plus(x: Int)(y: Int): Int = x + y // a function of type Int => (Int => Int)
plus(5) // a function of type Int => Int
plus(5)(3) // 8
```

Curried functions are so common in functional programming that the => that represents function types is typically assumed to be right-associative: Int => (Int => Int) is simply written Int => Int => Int. For example, the function

```
def lengthBetween(low: Int)(high: Int)(str: String): Boolean =
  str.length >= low && str.length <= high
```

has type Int => Int => String => Boolean. You can use it to produce a Boolean, as in

```
lengthBetween(1)(5)("foo") // true
```

but also to produce other functions:

```
val lengthBetween1AndBound: Int => String => Boolean = lengthBetween(1)
val lengthBetween1and5: String => Boolean = lengthBetween(1)(5)

lengthBetween1AndBound(5)("foo") // true
lengthBetween1and5("foo") // true
```

Before closing this section on currying, we should consider a feature that is particular to Scala (although other languages use slightly different tricks for the same purpose).