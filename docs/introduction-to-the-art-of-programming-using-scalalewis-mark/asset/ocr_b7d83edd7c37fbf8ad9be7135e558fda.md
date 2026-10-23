# 8.3.2 yield

The while loop is a statement only and can not be used as an expression. This is not true of the for loop. You can cause the for loop to produce a value so that is can be used as an expression. This is done by putting the yield keyword right after the close parentheses of the for loop. When you use yield, instead of a statement you need to have an expression. The result of the for expression is a new collection with all of the yielded values in it. The following shows a simple example of this.

```
```
scala> for(i <- 1 to 10) yield i*i
res22: scala.collection.immutable.IndexedSeq[Int] =
Vector(1, 4, 9, 16, 25, 36, 49, 64, 81, 100)
```
```

Another slightly different example shows how you could use a for loop to make a collection that is filled with values read in from input.

```
```
val nums=for(i <- 1 to 10) yield readInt()
```
```

This could work as an alternative to fill if you find it more readable.

You should note that the example gives a result with a type we have not seen before. The general type is listed as an IndexedSeq[Int] and the specific object is a Vector[Int]. Do not let these different types throw you off. For our purposes, we will use them just like we would the Array type. The difference between the Array and the Vector is that the Vector is immutable. You can index into it efficiently like an Array, but like a List, you are not allowed to change the values of the elements. All the standard functions that we saw earlier for Array and List will work on these types as well.

# 8.3.3 if Guards

The for loop in Scala also allows conditionals. After the first generator, you can put an if that has a condition on it. The for loop will only happen for those instances where the condition is true. This can lead to a more compact syntax than putting a if inside of the for loop. It can also be more efficient. Most importantly, it can be useful when you have a yield so that you do not add unwanted elements to the value of the expression.

As an example of this, and other aspects of the for loop, let us consider having a sequence of points in 2-D that are stored as (Double,Double). I want an expression that will give me back a sequence that has the distances to those points. The catch is that I only want the distances that are less than one. Without the if guard, this would require two steps. One would calculate the distances and a second would filter out the large values. The if guard lets us do this in a single loop.

```
```
for((x,y) <- points; if magnitude(x,y)<1.0) yield magnitude(x,y)
```
```

This example was written assuming a function called magnitude that might look like the following.

```
```
def magnitude(x:Double,y:Double):Double = math.sqrt(x*x+y*y)
```
```

The beginning of this loop illustrates how you can use a pattern on a tuple to pull out the two elements in the point. This is actually one of the great strengths of the for loop in Scala that helps simplify your programming.