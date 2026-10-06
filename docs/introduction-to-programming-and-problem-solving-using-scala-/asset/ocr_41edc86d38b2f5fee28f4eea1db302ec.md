# Functions

Now substitute for the endurancePoints function call using the value 36 for numLaps.

```
45 + {
  if (36 < 20) 0
  else if (36 > 40) 20
  else 36-20
}
```

The first condition is false, so that if is replaced by the false expression, after the first else.

```
45 + {
  if (36 > 40) 20
  else 36-20
}
```

The next condition is also false, so that also simplifies to the false expression.

```
45 + {
36-20
}
```

At this point, all that is left to do is math with literals, so we get 45 + 16, which simplifies to our final answer of 61.

# Higher Order Functions

Function literals would be nothing more than a novelty in Scala or any other programming language if it were not for higher order functions. A higher order function is a function that operates on other functions. This means that we pass other functions into it, or results in a function. Higher order functions are functional programming concept, and they can be challenging to get ones ahead, but we will see how they can be used in a higher order function here, in the coming chapters.

As an example of, f(c) and g(x), then the composition of f with g is f(g(x)). We will write a Scala function that does this as follows:

```
scala def compose(f:Double => Double, g:Double => Double) => Double =
  x => f(g(x))
compose: (f:Double => Double, g:Double => Double) => Double =
```

Note that we write the function types themselves using arrows, "rocket". We could call this with functions we build using def or function literals. We will do it first with the two functions that have been defined using def.

```
scala def plus5(x:Double):Double = x+5
plus5:(x: Double)Double
```

```
scala def square(x:Double):Double = x*x
square: (x: Double)Double
```

Now we want to compose to build new functions from these two using the compose function and then see our new functions working.