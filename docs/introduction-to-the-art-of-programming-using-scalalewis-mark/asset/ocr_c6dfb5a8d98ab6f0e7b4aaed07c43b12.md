So while we wrote operateOnList and operateOnArray to do sums and products of those collections, Scala would have allowed us to simply call the sum or product methods as is seen here.

```
scala> lst.sum
res2: Int = 30
```

```
scala> lst.product
res3: Int = 4536
```

The requirement that the values be numeric means that while you can concatenate Strings with +, you can not put them together with sum. For a List[String] or Array[String], you should use mkString to concatenate the values.

# 7.4.2 Higher-Order Methods

While you might feel like the list of methods shown here is quite a lot and gives us many capabilities, we have not yet hit on the real power of the Scala collections. All of these methods have taken normal values for arguments. Just like our first recursive methods, they can be made more powerful by adding some abstraction and making them higher-order methods. Below is a list of many of the higher-order methods that are part of the sequences in Scala. The type A is the type that is contained in the List or Array. The type B could be any other type.

+   - count(p:(A)=>Boolean) -- Takes a function that will operate on an element and return a Boolean. Returns the number of elements in the collection for which this returns true.

```
scala> lst.count(_>5)
res0: Int = 3
```

+   - dropWhile(p:(A)=>Boolean) -- Takes a function that will operate on an element and return a Boolean. Returns a new collection that contains all elements after the first group for which that function is true.

```
scala> lst.dropWhile(_>3)
res0: List[Int] = List(3, 9, 1)
```

+   - exists(p:(A)=>Boolean -- Takes a function that will operate on an element and return a Boolean. Returns true if there is some element in the collection for which the function is true.

```
scala> lst.exists(x => x>4 && x<7)
res0: Boolean = true
```

+   - filter(p:(A)=>Boolean) -- Takes a function that will operate on an element and return a Boolean. Returns a new collection that contains only the elements for which the function is true.

```
scala> lst.filter(_<5)
res0: List[Int] = List(4, 3, 1)
```