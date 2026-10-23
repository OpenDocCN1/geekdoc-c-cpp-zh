In top level of script after getAndClear:

![](bbox=[0.25, 0.12, 0.8, 0.25])

**FIGURE 7.6:** The configuration of memory after *getAndClear* has executed.

braces and has two lines. The first line is a `val` that pulls the two parts out of the tuple. The number from the `List` is called **n** and the index is called **i**. The function literal finished with an `if` expression that checks the index and gives the value of 0 or **n** based on if **i** is the same as `index`. There are other ways to write this. One that could be more efficient when `index` is small compared to the length of the `List` is shown here.

```
```scala
def getAndClear2(lst:List[Int], index:Int): (Int, List[Int]) = {
  (lst(index), lst.take(index)::(0::lst.drop(index+1)))
}
```
```

This version uses the cons operator, `::`, which we saw before. It adds one new element to the front of a `List` and gives that back. It also uses an operator that we have not seen previously, the `:::` operator. This does roughly the same thing as `::` except that the argument on the left is a full `List` that should be appended to the front of the second `List`.

Of course, because the `List` version is having to rebuild the `List`, it could go a step further and truly clear the value. It could remove it from the `List` instead of overwriting it with zero. This would be done with `filter` instead of `map` on the first version. The second version is even easier to change. We leave that as an exercise for the reader to create and try.

An interesting question now becomes which of these is better? Is it better to use an `Array` which can be mutated or a `List` which can not? The answer is that it depends on whether you want a function to be able to mutate the data. If the function is supposed to mutate the data then there can be a speed benefit to passing something mutable. However, if you do not want the data mutated then there is a problem with passing mutable data. When you pass mutable data into a function, you have no control over whether it is mutated. In situations where you do not want your data mutated, this requires that you make a **DEFENSIVE COPY**. To protect your version of the data, you make a copy of it and pass the copy into the function.

For this reason, the question of whether you want to use a mutable or immutable structure depends a lot on the way in which you use that data. If it is going to be mutated frequently then it might make sense for it to be mutable. However, if it is not going to be mutated frequently then immutable likely makes sense so you do not have to make defensive copies. Even in situations where there might be a fair bit of mutation, you need to consider how much defensive copying will be needed if you choose mutable.