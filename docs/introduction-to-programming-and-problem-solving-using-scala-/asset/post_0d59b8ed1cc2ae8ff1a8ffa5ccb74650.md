
# Introduction to Programming and Problem-Solving Using Scala

The behavior of these examples might seem more obvious. As you can see, in the second example you entered 1, 2, and 3 as values. This is what we started off the chapter doing: functions to read values into an Array or List. It turns out that as we know how many elements we have, we can do this with a single line of code using fill.

To see how pass-by-name is used here, consider the following function that is intended to fill a List similar to the first example.

```scala
def fillList(n:Int,x:Double):List[Double] = if (n==1) Nil else x :: fillList(n-1,x)
```

We call this function passing how many numbers we want in the List, and what value we want to use. Here is what happens if we call it with 5 and `math.random`.

```scala
scala> fillList(5,math.random)
res29:List[Double] = List(0.5701406699076761, 0.5701406699076761, 0.5701406699076761, 0.5701406699076761, 0.5701406699076761)
```

Unlike the fill, all values in this List are the same. If we had called it `readDouble`, only one value would have read in all, and all the elements would have that one value. Pass-by-name is how fill is able to get different values in those examples.

```scala
scala> Array.fill(4){ println("Evaluating argument"); 5 }
Evaluating argument
Evaluating argument
Evaluating argument
Evaluating argument
res30:Array[Int] = Array(5, 5, 5, 5)
```

Note that the second argument has been put in curly braces only. As a general rule, Scala allows you to do that for an array list that has only one argument. This is part of the reason fill is called. You can add an extra of parentheses, but you will still need the curly braces because this is a block of code with two expressions in. This example is illustrative, but not all that useful. A more interesting example uses a var.

```scala
scala> var i=1
Int: Int = 1
scala> List.fill(5){ i::= i }
res31:List[Int] = List(2, 4, 8, 16, 32)
```

Here the var is initialized to 1. The value argument multiplies i by 2 and stores value back in. Then it gives it back as the value to use. You can see there are situations where this could be helpful, but this method of filling an array with powers of two is likely to confuse most people reading your code.

The primary limitation with fill is that the code in generally does not know what element of the sequence is being generated. Sometimes that information can be helpful. That is why the tabulate method exists. The tabulate method creates a new list or array filling each element with its index by a function that you apply to it. Tabulate much like you fill, the second argument is not a pass-by-name variable, it is a function that takes an Int and results in the type that the sequence should be filled with. A simple example is a List that is filled with elements that are the squares of their indices. This can be produced by the following code.

```scala
scala> List.tabulate(5)(i => i*i)
```

# Arrays and Lists in Scala

res32: List[Int] = List(0, 1, 4, 9, 16)

A more complex example would fill an Array with the result of evaluating a polynomial on each index.

```scala
scala> Array.tabulate(6)(x => 3*x*x+5*x-7)
res33: Array[Int] = Array(-7, 1, 15, 35, 6, 93)
```

This fills the array with values of $3x^2-7$ where $x$ is the index: 0, 1, 2, 3, 4, and 5.

> Note: You can also make larger Arrays calling new. If you have any experience with other languages, you might be familiar with this approach. It is generally not the recommended approach in Scala, as it is prone to cause certain types of exceptions.

## 6.5 Standard Methods

Now you know how to make Arrays and Lists. In order to do things with them, you need to know what methods are available on. One of the strengths of the Scala collections is that they have rich interfaces. An interface is a set of protocols, routines, and tools for building software applications. Scala's interfaces have a lot of different methods in them. We looked at length and size on the Array and head and tail on the List, but this was only scratching the surface. You can actually call either of them on Lists or Arrays. However, length and size are efficient for Arrays while tail is inefficient on the Array. In this section we will run through all the other methods that are available to us when working with Lists and Arrays. We will start with the simple.

## 6.5.1 Basic Methods

We break the methods into a few groups based on what they do. Inside of each group the methods are what they give you a new collection result in a collection of the type that it is called on. So if you call them on an Array, you get an Array; if you call them on a List, you get a List.

- `drop(n)`: Returns the collection excluding the first $n$ elements.
- `take(n)`: Returns the collection with the first $n$ elements.
- `head`: Returns the first element of the collection.
- `tail`: Returns the collection excluding the first element.
- `init`: Returns the collection excluding the last element.
- `last`: Returns the last element of the collection.
- `size`: Returns the number of elements in the collection.
- `length`: Returns the number of elements in the collection.
- `slice(from, to)`: Returns a sub-section of the collection from `from` to `to`.
- `contains(elem)`: Returns true if the collection contains the element.
- `startsWith(seq)`: Returns true if the collection starts with the specified sequence.
- `endsWith(seq)`: Returns true if the collection ends with the specified sequence.
- `isEmpty`: Returns true if the collection has no elements.
- `nonEmpty`: Returns true if the collection has at least one element.
- `filter(p)`: Returns a collection containing only the elements that satisfy the predicate `p`.
- `map(f)`: Returns a new collection where each element has been transformed by function `f`.
- `fold(z, f)`: Reduces the collection to a single value using a binary function starting with initial value `z`.
- `foldLeft(z, f)`: Reduces the collection from left to right.
- `foldRight(z, f)`: Reduces the collection from right to left.
