
Now we will look at the Set, Map, and Buffer types. These types can give you a significant boost in your programming and make it much easier to do certain tasks.

## 20.2 Sets

The concept of a set comes from math. There are two main differences between the Set type and the Seq type. The most important one is that a Set does not allow duplicate values. If you add something to a Set and there is already something there that is equal to it, it does not add a new value and the size of the resulting set is the same as what you had before. The other difference is that the order of elements in a Set is not guaranteed.¹ We can see both of these effects in the following sequence of REPL commands.

¹ If you happen to be using a SortedSet, then the order of the objects will match the natural ordering of the type, but this is more the exception than the rule.

```scala
scala> Set(1,2,3)
res0: scala.collection.immutable.Set[Int] = Set(1, 2, 3)

scala> res0 + 4
res1: scala.collection.immutable.Set[Int] = Set(1, 2, 3, 4)

scala> res1 + 2
res2: scala.collection.immutable.Set[Int] = Set(1, 2, 3, 4)

scala> res1 + -10
res3: scala.collection.immutable.Set[Int] = Set(-10, 4, 1, 2, 3)
```

This begins with a set that has the values 1, 2, and 3. As with the List and Array types, Scala figures out that this is a Set[Int]. You can also see from the inferred type that by default we get an immutable set.

You can add to a set with +, you get back a new set that has the element after the plus sign added in. The second statement gives us back a set that includes 4 in addition to the 1, 2, and 3. In the third command we add a 2 to this new set. The result looks the same as the set before the 2 was added. This is because the set cannot contain duplicate elements.

The last statement adds the value -10 into the set from res1. This value goes into the resulting set because there had not been a -10 previously. However, the result shows that order is not preserved in sets. Adding the -10 into the set not only put it in an odd place at the beginning, it also altered the location of the 4 in the set. From this you can see that you want to use sets when what you care about is the uniqueness of elements, not the order in which you get them.

The fact that the order can change means that "indexing" into a set in the manner we have done with an Array or a List does not have much meaning. You can perform that type of operation on a Set, but the meaning is a bit different. Consider the following examples.

```scala
scala> res3(2)
res4: Boolean = true

scala> res3(5)
res5: Boolean = false

scala> res3(-10)
res6: Boolean = true
```

This type of operation on a set does not give you back a value at a particular location. Instead, it returns a Boolean that tells you whether or not the specified value is in the set. This works equally well if the set contains values other than Ints. Consider the following.

```scala
scala> val strSet=Set("Mark","Jason","Kevin")
strSet: scala.collection.immutable.Set[java.lang.String] = Set(Mark, Jason, Kevin)

scala> strSet("Jason")
res7: Boolean = true

scala> strSet("Bill")
res8: Boolean = false
```

In this example, the set contains Strings and the "indexing" is done by passing in Strings. The meaning is the same either way. The return value is true if the argument passed in is in the set and false if it is not. To see why this works this way, go look in the Scala API at one of the versions of Set. They all have a type parameter called A and they define the following method.

```scala
def apply (elem: A): Boolean
```

Remember that apply is a special method that is invoked when an object is used with function call notation. So f(5) in Scala gets expanded to f.apply(5). Here the apply takes one argument, elem, which must have the type A. That is the type parameter of the set as a whole, so you have to pass in an object of the type that the set contains. This method then returns to you a Boolean telling you whether or not that value is in the set.

### 20.2.1 Running Through Sets

In addition to the standard higher order methods like map, filter, and foreach, that are available for both Set and the sequences that we have worked with previously, the Set type works perfectly well with for loops as well.

```scala
scala> for(v <- res3) println(v)
1
2
-10
3
4
```

In fact, you cannot really use a while loop to run through a Set, because you cannot index by position. Also, the order in which the loop runs through the set values is not something you can predict. It does not even have to match the order that the values are displayed when the Set is converted to a String for printing.

### 20.2.2 Mutable vs. Immutable

The examples above showed the default immutable Set type. Like the List type that we saw previously, an immutable set does not change after it is created. When we add elements to the set with the + operator, we get back a new set and the original set is unaltered. We can demonstrate this by calling back up the original set.

- `--=(xs : TraversableOnce[A])` - Removes all the elements in xs from the set.
- `add(elem : A) : Boolean` - Adds the specified element to the set. Returns true if it was not there before the call and false otherwise.
- `clear() : Unit` - Removes all elements from the set.
- `remove(elem : A) : Boolean` - Removes the specified element from the set and returns true if it was there to remove or false otherwise.
- `retain(p : (A) => Boolean) : Unit` - Removes all elements that do not satisfy the predicate from the set.

Mutable sets can also be updated using assignment. This is basically the inverse operation of "indexing" that we saw before using apply. The index is the value you are adjusting in the set and the assignment is either to true or false. To see how this works, consider the following examples.

```scala
scala> mset(7)=true

scala> mset(2)=false

scala> mset
res14: scala.collection.mutable.Set[Int] = Set(1, 4, 7, 3)
```

The first line adds 7 to the set while the second removes 2. This works because the scala.collection.mutable.Set type defines an update method that looks like this.

```scala
def update (elem: A, included: Boolean): Unit
```

So the line mset(7)=true gets expanded to mset.update(7,true).

Earlier in this section it was mentioned that the standard methods, like map and filter, will do the same thing on a mutable set as they do on an immutable set. This was very intentional. The same operations on subtypes like this should always have the same outward appearance and significant effects. This reduces the chances of programmers making silly mistakes. If you want to mutate the set you have to call one of the specific methods for doing so. For example, you would call retain instead of filter. If you accidentally try to use one of these operations on an immutable type the code will not compile. If the operations with the same name had different behaviors, it would be very easy for the programmer to introduce logic errors because he/she believed an object was one type when it was actually another, or for bugs to be introduced later on by a programmer changing the specific type that is assigned to a variable.

### 20.2.3 Using a Set

To see how the Set type can be useful we will write a function that tells us all the unique words in a text file. The function will take the name of the file as an argument and return a Set[String] that has all the words in lowercase. As with any function of any significance, this can be done in many ways. We are going to do it making heavy use of the Scala collection methods. The fact that we are using the collection methods makes it more sensible to use a Source than a Scanner. Here is code that will do this.

```scala
def uniqueWords(fileName:String):Set[String] = {
  val source = io.Source.fromFile(fileName)
  val words = source.getLines.toSeq.flatMap(_.split(" +"))
    .map(_.filter(_.isLetter).toLowerCase).toSet
  source.close()
  words
}
```

A function is defined using the signature that was described. This function includes only four statements. The first and third statements in the function open the file and close it. The last statement is just an expression for the set that was created from the source. The second statement is where all the work is done and is worth looking at in detail.

This line declares the variable words and makes it equal to a set of the words. To do that it gets the lines from the source and turns them into a sequence. The toSeq call makes types work out better with flatMap. As you might recall, getLines returns an Iterator. The Iterator type is a collection that you can only pass through once. It is consumed during that pass. By bumping it up to a sequence we get something that works better with the Array[String] that we get from the split method.

After the lines are converted to a sequence there is a call to flatMap. This is one of the standard higher-order methods on collections. We have not used it much so it is worth taking a minute to discuss. As you can tell from the name, flatMap is closely related to map. The map method takes each element of a collection, applies some function, and makes a new collection that has the results of that function application. The flatMap does basically the same thing only it expects that the function passed in is going to return collections. Instead of returning a collection of collections, as map would do, flatMap will flatten out all of the inner collections into one long collection. If you use map on the sequence of lines and use the same map function, you will get a Seq[Array[String]]. Each element of the sequence will contain an array of the words from that line. However, that is not quite what we want. We want a simple sequence of words, not a sequence of arrays of words. This is what flatMap does for us. It puts each of the arrays end to end in the new sequence so that we get a Seq[String].

If we knew that the file only included simple words in lowercase we could stop there. However, most text files will include capitalization and punctuation as well. This would mess up the set because "Hi" is not equal to "hi" and they both would appear in the result when we want only one. Similarly, the word "dog" would be different than "dog." or "dog," if the word happened to appear directly before a punctuation mark. The second line of the second statement includes logic to deal with this. Each of the words that the file was broken into is passed through a map. That map filters out any non-letter characters and converts the resulting strings to lower case. The filtering of non-letter characters is perhaps too aggressive because it removes things like apostrophes in contractions, but the result it provides is sufficiently correct for our purposes.

The last thing that happens in the second statement is that the sequence is converted to a Set. This gives us the type we desired and removes any non-unique elements by virtue of being a Set.

## 20.3 Maps

Another collection type that is extremely useful, probably more so than the Set in most programs, is the Map. Like the Set, the term Map has origins in math. A mapping in mathematics is something that takes values from one set and gives back values from another set. A function in math is technically a mapping. The Map collection type is not so different
