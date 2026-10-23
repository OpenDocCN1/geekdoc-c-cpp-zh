
In top level of script after getAndClear:

![](img/157fcf510c119278e4b1267c62717fa8_199_0.png)

**FIGURE 7.6:** The configuration of memory after *getAndClear* has executed.

braces and has two lines. The first line is a `val` that pulls the two parts out of the tuple. The number from the `List` is called **n** and the index is called **i**. The function literal finished with an `if` expression that checks the index and gives the value of 0 or **n** based on if **i** is the same as `index`. There are other ways to write this. One that could be more efficient when `index` is small compared to the length of the `List` is shown here.

```scala
def getAndClear2(lst:List[Int], index:Int): (Int, List[Int]) = {
  (lst(index), lst.take(index):::(0::lst.drop(index+1)))
}
```

This version uses the cons operator, `::`, which we saw before. It adds one new element to the front of a `List` and gives that back. It also uses an operator that we have not seen previously, the `:::` operator. This does roughly the same thing as `::` except that the argument on the left is a full `List` that should be appended to the front of the second `List`.

Of course, because the `List` version is having to rebuild the `List`, it could go a step further and truly clear the value. It could remove it from the `List` instead of overwriting it with zero. This would be done with `filter` instead of `map` on the first version. The second version is even easier to change. We leave that as an exercise for the reader to create and try.

An interesting question now becomes which of these is better? Is it better to use an `Array` which can be mutated or a `List` which can not? The answer is that it depends on whether you want a function to be able to mutate the data. If the function is supposed to mutate the data then there can be a speed benefit to passing something mutable. However, if you do not want the data mutated then there is a problem with passing mutable data. When you pass mutable data into a function, you have no control over whether it is mutated. In situations where you do not want your data mutated, this requires that you make a **DEFENSIVE COPY**. To protect your version of the data, you make a copy of it and pass the copy into the function.

For this reason, the question of whether you want to use a mutable or immutable structure depends a lot on the way in which you use that data. If it is going to be mutated frequently then it might make sense for it to be mutable. However, if it is not going to be mutated frequently then immutable likely makes sense so you do not have to make defensive copies. Even in situations where there might be a fair bit of mutation, you need to consider how much defensive copying will be needed if you choose mutable.

## 7.9 Pass-By-Name

Earlier we looked at the way in which arguments are passed in Scala. This is a style called PASS-BY-VALUE. The function gets a copy of what the variable was in the calling code. The function can not change that variable, it can only change what it refers to if what it refers to is mutable. Some languages provide an alternate way of passing things called PASS-BY-REFERENCE. When something is passed by reference, the function has the ability to change the variable in the calling function itself. The fact that all variables in Scala basically are references blurs the line between the two, but fundamentally Scala only allows pass-by-value and the function can only modify things seen to the outside if the variable refers to a mutable object.

While Scala does not provide a true pass-by-reference, it does provide a passing style that few other languages provide, PASS-BY-NAME. The idea of pass-by-name is that the argument is passed not as a value, but as a THUNK that is basically a set of code that will be executed and give a value when the parameter is used in the function. You can imagine pass-by-name as automatically creating a function that takes no argument and returns a value that will be executed each time the argument is used. To help you understand this and see the syntax, we will give a simple example. We will start making a basic increment function in the way we are used to doing.

```scala
scala> def incr(n:Int):Int = {
  | println("About to increment.")
  | n+1
  | }
incr: (n: Int)Int
```

The print statement is just to help us keep track of what is happening when. Now we will write the same function again, but this time pass the argument by name instead.

```scala
scala> def incrByName(n : =>Int):Int = {
  | println("About to increment.")
  | n+1
  | }
incrByName: (n: => Int)Int
```

The syntax for passing an argument by name is to put a rocket before the type of the argument. This is the same arrow used in function literals. If we were to put empty parentheses in front of it to get `()=>` we would have the type of a function that takes no arguments and returns an Int. The by-name argument is much the same only when you call the function you do not have to explicitly make a function. To start off, we will call this function in the simplest way we possibly could.

```scala
scala> incr(5)
About to increment.
res0: Int = 6

scala> incrByName(5)
About to increment.
res1: Int = 6
```

No surprises here. They appear to both do the same thing. Both print the statement and give us back 6. However, the two are not really doing the same thing. To make that clear, we will call them again and have the argument be a block that includes a print.

```scala
scala> incr({println("Eval"); 5})
Eval
About to increment.
res2: Int = 6

scala> incrByName({println("Eval"); 5})
About to increment.
Eval
res3: Int = 6
```

Now it is clear that they are not doing the same thing. When you pass an argument by value, it is evaluated before the function starts so that you can have the value to pass through. When you pass by name, the evaluation happens when the parameter is used. That is why the line “Eval” printed out after “About to increment.” in the second case. The println in the function happens before the value of n is ever accessed.

Using pass-by-name gives you the ability to do some rather interesting things when mutations of values come into play. To see that, we can write a slightly different function.

```scala
scala> def thriceMultiplied(n : => Int):Int = n*n*n
thriceMultiplied: (n: => Int)Int
```

It might seem that this method should be called cubed, but as we will see, this might not always apply for it because it uses pass-by-name. To start with, let us call it with an expression that gives a simple value, but prints something first.

```scala
scala> thriceMultiplied({println("Get value."); 5})
Get value.
Get value.
Get value.
res4: Int = 125
```

Note that the println statement happened three times. This is because the value n was used three times in the function. Had the parameter not been passed by-name, that would not have happened. It would have printed once, when the function was called. Try this for yourself.

This particular call still gave us a valid cube though. So why was the function not simply called cube? The reason is that if the code in the argument does the right thing, the result won’t be a cube. Here is an example.

```scala
scala> var i=5
i: Int = 5
```

```scala
scala> thriceMultiplied({i+=1; i})
res5: Int = 336
```

336 is not a perfect cube. So how did we get this value? In this example we introduced a var. The code in the pass-by-name argument alters this var. As a result, every time that n is used, the value given by n is different. The first time we use n the value is 6 because the original 5 was incremented and then returned. The next time it is 7 because the 6 that it was set to the previous time is incremented again. The last time it is 8. So the answer is 6 * 7 * 8 = 336.

These calls with both parentheses and curly braces might seem odd. The creators of Scala thought so. As a result, they made it so that if a function or method takes an argument list with only one value in it, that value can be in curly braces instead of parentheses. This allows a shorter syntax for the call that looks like this.

```scala
scala> thriceMultiplied {i+=1; i}
res6: Int = 990
```

You might be tempted to think that leaving off the parentheses changed what happened because the result is different. It was not the parentheses though. Remember that after the last call i had been incremented up to 8. So this time the result was 9 * 10 * 11 == 990.

## 7.10 Fill and Tabulate

One of the reasons for introducing pass-by-name in this chapter is that there are some other ways to make Arrays and Lists. One of them uses pass-by-name. Previously we saw how we could follow Array or List with a list in parentheses to get back either an Array or a List with those values in it. We could also use `new` to get a large array of default values or `::` to put together Lists. There are also methods we can call on Array and List called `fill` and `tabulate`. Both can be used to make a new Array or List. They both work well for making large Arrays and Lists, unlike the version where you have to specify the individual values. Let us look at how these work.

The fill method is a curried method that takes a first argument specifying how many elements to make and a second argument, which is a pass-by-name argument giving the value. The simplest invocation of this might look like the following.

```scala
scala> Array.fill(10)(4)
res3: Array[Int] = Array(4, 4, 4, 4, 4, 4, 4, 4, 4, 4)

scala> List.fill(6)(23)
res4: List[Int] = List(23, 23, 23, 23, 23, 23)

scala> List.fill(6)("hi")
res5: List[java.lang.String] = List(hi, hi, hi, hi, hi, hi)
```

If the second argument is a constant, then the call simply fills the whole Array or List with that value. However, that argument is passed by-name so it is actually re-evaluated for each element of the sequence and if it has side effects, they will happen multiple times. The easiest way to see this is to have the second argument print something.

```scala
scala> Array.fill(4){ println("Evaluating argument"); 5 }
Evaluating argument
Evaluating argument
Evaluating argument
Evaluating argument
res6: Array[Int] = Array(5, 5, 5, 5)
```

Note that here the second argument has been put in curly braces only. Remember that Scala allows you to do that for an argument list that only has one argument. You can add an extra set of parentheses, but you will still need the curly braces because this is a block of
