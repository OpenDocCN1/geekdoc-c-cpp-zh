# 8.3.3 if Guards

The for loop in Scala also allows conditionals. After the for loop generator, you can put an if that is followed by a condition. The for loop will only happen for those instances the condition is true. This can lead to a more compact syntax than putting an inside of the for loop. It can also be more efficient. Most importantly, it can be useful when you have a yield so that you do not add unwanted elements to the value of the expression.

As an example of this, and other aspects of the for loop, let us consider having a sequence of points in 2-D that are stored as (Double,Double). We want an expression that will give us a back that has the distances to those points from the origin. The catch is that we want the distances that are less than one. Without the guard, this would require two steps. One would calculate the distances and a second would filter out the large values. The if guard lets us do this in a single loop

```
for ((x,y) <- points; if magnitude(x,y)<1 yield magnitude(x,y)
```

This example written assuming a function called magnitude might look like the following.

```
def magnitude(x:Double,y:Double):Double = math.sqrt(x*x+y*y)
```

The beginning of this loop illustrates how you can use a pattern to pull out the two elements in the point. This is actually one of the strengths of the for loop in Scala that helps simplify your code.

> Syntax Note
Note that you do not have to include parentheses after the if in an if guard. You can, unlike a normal if it is not required.

The one significant drawback of this approach is that the magnitude function is called twice so this is less than ideal. We will see how to get around that shortly.

# 8.3.4 Multiple Generators

The for loop in Scala also supports the ability to iterate across multiple collections in a single loop. This can be done by putting more than one variableName <- collection in the parentheses. We call these generators. Each that you put into the for will generate values from the collection to run through the logic. The first generator will pull the first value from its collection. A second generator will then run through all of its values before the first one goes on the second option. The number of times the body of the loop happens as the product of the number of elements in the collections for the generators, not some. To help you understand this, consider the following example.

```
scala for (i <- 1 to 5; c <- 'a' to 'c') println(""+i+" "+c)
a1
b1
a2
b2
c
```