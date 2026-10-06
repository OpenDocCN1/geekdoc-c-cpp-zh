# Type Basics and Argument Passing

function passing it two arguments separately. In the third line, we call add and pass it the argument 5. We store the result of this in a variable plus5. Note that plus5 is actually a function that takes an integer and returns an integer. At the end we call plus5 and pass the value 6 which gives us back.

This example shows what it means to curry a function. There can be times when this approach is quite useful. For that reason, Scala provides a shortcut for doing it. If you define a function and follow it with more than one argument list, the function is curried. So, the code above could be entered like this:

```
scala def add(x:Int)(y:Int) = x+y
add: (x:Int) => (y:Int) => Int
scala add5(6)
res2: Int = 11
```

```
scala val plus5 = add5()
plus5: (Int) => Int = <function1>
scala plus5(6)
res3: Int = 11
```

The only difference here is the underscore where the second argument list you really meant to specify the first argument when we make plus5. This tells Scala that currying is not hard to do in Scala. Hopefully these examples made it clear why you would. We have actually seen two things in this chapter that can provide the motivation to curry a function. The first was in the section on variable length arguments for tests, assignments and quizzes because a variable length argument can only be used with the last argument in an argument. One way around this is to curry the function each type of grade to be its own argument list. That would produce the following:

```
def courseAverage(tests:Double)(assns:Double)(quizzes:Double):Double = {
val aveTest = average(tests:*)
valAssns = average(assns:*)
val aveQuiz = averagedDropMin(quizzes:*)
fullA(aveTest,aveAssns,aveQuiz)
}
```

Notice that you still need the :* when passing the arguments through other functions that have variable length arguments. This version allows us to invoke the function like this.

courseAverage(80,95,100)(100,80)(56,78,92)

So currying gives us the ability to have more than one variable argument list in a single function.
The other place in this chapter where we have introduced something that might benefit from currying was right before the section on currying in the aside of code blocks arguments. The syntax when you leave off parentheses and only use curly braces works when an argument list has a single argument. This means that we could never take advantage of this feature for any function that needs more than one argument.

> ⁹There are actually several reasons why one might choose to curry a function that goes beyond the scope of this book.