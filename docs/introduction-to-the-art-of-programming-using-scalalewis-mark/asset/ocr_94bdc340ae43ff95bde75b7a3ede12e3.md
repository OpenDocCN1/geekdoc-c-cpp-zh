```
}
mainGrades
}
```

This begins with the printMenu function which simply prints a menu. The only thing of interest here is the use of the triple quote string so that the string can be made to span multiple lines. If you do not do this, you will have to use `\n` to denote line breaks.

In this imperative version, the printMenu function is followed by the declaration of three variables. They are all vars and they are of the type List[Double]. The have to be vars because the List itself is immutable. So whenever something is added we have to change the variable reference and point to a new List. Remember, this can be done efficiently for the List type so that is fine.

If you type this code in and play with it a bit, you will probably find that you can make it behave poorly. In particular, you can get it so that when you ask for the average you get an output like this.

The average is NaN

This should lead you to two questions. First, what is this thing called NaN? Second, what is causing this? Technically the second matters more because we need to know that to fix it. However, knowing the answer to the first can help you figure it out if you were not able to do so from your testing. The Double type, as we have discussed previously, is used to represent numeric values that have fractional parts. It has a rather large range and good precision, but it is technically a fixed precision type. You can not represent any real number with it. In addition, some mathematical operations produce results that are not well defined. Consider the following.

```
scala> 1.0/0.0
res2: Double = Infinity

scala> -1.0/0.0
res3: Double = -Infinity
```

You should have learned in a math class that you can not divide by zero. If you do this with Ints you get an error. However, if you do it with Doubles you get what you see here. Any operation that goes outside the range of the Double will also get you either Infinity or -Infinity, depending on which side of the range it goes out on as is shown here.

```
scala> 1e150*1e200
res6: Double = Infinity
```

What does all of this have to do with NaN? Well, NaN stand for “Not-a-Number” and it is the result of an operation when it is not clear what the result should be. One way to get this is to add Infinity and -Infinity or do other operations with Infinity or -Infinity that the computer can not know the result of. Consider this example.

```
scala> 1e150*1e200-1.0/0.0
res10: Double = NaN
```

In general the computer can not know if this would be out of range on the positive or negative so it goes to NaN because it gives up. There is one other way to get a NaN: divide zero by zero.

```
scala> 0.0/0.0
res11: Double = NaN
```