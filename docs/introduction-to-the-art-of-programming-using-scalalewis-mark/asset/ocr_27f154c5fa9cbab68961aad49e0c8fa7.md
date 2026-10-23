```
scala> res3(-10)
res6: Boolean = true
```

This type of operation on a set does not give you back a value at a particular location. Instead, it returns a Boolean that tells you whether or not the specified value is in the set. This works equally well if the set contains values other than Ints. Consider the following.

```
scala> val strSet=Set("Mark","Jason","Kevin")
strSet: scala.collection.immutable.Set[java.lang.String] = Set(Mark, Jason, Kevin)
```

```
scala> strSet("Jason")
res7: Boolean = true
```

```
scala> strSet("Bill")
res8: Boolean = false
```

In this example, the set contains Strings and the “indexing” is done by passing in Strings. The meaning is the same either way. The return value is true if the argument passed in is in the set and false if it is not. To see why this works this way, go look in the Scala API at one of the versions of Set. They all have a type parameter called A and they define the following method.

```
def apply (elem: A): Boolean
```

Remember that apply is a special method that is invoked when an object is used with function call notation. So f(5) in Scala gets expanded to f.apply(5). Here the apply takes one argument, elem, which must have the type A. That is the type parameter of the set as a whole, so you have to pass in an object of the type that the set contains. This method then returns to you a Boolean telling you whether or not that value is in the set.

# 20.2.1 Running Through Sets

In addition to the standard higher order methods like map, filter, and foreach, that are available for both Set and the sequences that we have worked with previously, the Set type works perfectly well with for loops as well.

```
scala> for(v <- res3) println(v)
1
2
-10
3
4
```

In fact, you can not really use a while loop to run through a Set, because you can not index by position. Also, the order in which the loop runs through the set values is not something you can predict. It does not even have to match the order that the values are displayed when the Set is converted to a String for printing.

# 20.2.2 Mutable vs. Immutable

The examples above showed the default immutable Set type. Like the List type that we saw previously, an immutable set does not change after it is created. When we add elements to the set with the + operator, we get back a new set and the original set is unaltered. We can demonstrate this by calling back up the original set.