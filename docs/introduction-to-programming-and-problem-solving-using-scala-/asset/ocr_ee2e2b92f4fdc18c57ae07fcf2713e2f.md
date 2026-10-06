# Functions

79

# Define a function

# Call a function

| function name | formal parameter | result type |
| --- | --- | --- |
| def square(x:Double):Double | = x*x |

| argument |
| --- |
| square (3) |

FIGURE 4.1: This figure shows examples of function definition and a function call.

# 4.3 Making and ways Using Functions

There are a number of ways to make functions in Scala. We will begin with the standard definition format. In chapter 2 we saw that we can use the keywords val and var to declare variables. In a similar way, we use the keyword def to define a function. We will start with the simple mathematical examples that were used in the previous section and Scala functions that match in the REPL.

```
scala def square(x:Double):Double = x*x
square: (x:Double)Double
```

In math, functions are given names f and g. This works for a limited context, but it does not scale up well if you are using a lot of different functions. We use the name square because it describes what the function does. The name is written the def and after we have a set of parentheses that contain a name and a type separated by a colon: like a val declaration that is called, it does not include an initial value¹ and the type is required. The value is specified when this function is called, just like for the math mathematical function, the type is Double. The contents of the parentheses are the formal parameters of the function.

After the parentheses is another colon and the type that this function gives back, or returns. In Scala we refer to this as the RESULT TYPE. In this case, because we are mirroring the mathematical function, the type is Double. After the result there is an equal sign and the expression x*x. Once this has been entered, the REPL tells us that we have created something like square with the type (x:Double)Double. This is Scala's way of telling us that we have a function that takes a Double and returns a Double.

Now that have defined square we can use it. In the last section we used our function with f(3). The syntax in Scala is the.

```
scala square(3)
res0: Double = 9.0
```

We give the name of the function followed by parentheses with the value we want to use for x. When we do this with the value 3, Scala gives back a value of 9.0 as a Double. This particular value could also be represented as an Int, but the function works with type Double and the Int that we passed in was converted to a Double and the result is also a Double.

> ¹Allows you to provide a value here, a default value. That is something you will not often; so, it is not counted until chapter 10.