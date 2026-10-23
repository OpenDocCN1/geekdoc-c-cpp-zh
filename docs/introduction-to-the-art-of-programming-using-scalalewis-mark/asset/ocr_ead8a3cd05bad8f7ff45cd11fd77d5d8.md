Now we will look at the Set, Map, and Buffer types. These types can give you a significant boost in your programming and make it much easier to do certain tasks.

# 20.2 Sets

The concept of a set comes from math. There are two main differences between the Set type and the Seq type. The most important one is that a Set does not allow duplicate values. If you add something to a Set and there is already something there that is equal to it, it does not add a new value and the size of the resulting set is the same as what you had before. The other difference is that the order of elements in a Set is not guaranteed. ¹ We can see both of these effects in the following sequence of REPL commands.

```
```
scala> Set(1,2,3)
res0: scala.collection.immutable.Set[Int] = Set(1, 2, 3)

scala> res0 + 4
res1: scala.collection.immutable.Set[Int] = Set(1, 2, 3, 4)

scala> res1 + 2
res2: scala.collection.immutable.Set[Int] = Set(1, 2, 3, 4)

scala> res1 + -10
res3: scala.collection.immutable.Set[Int] = Set(-10, 4, 1, 2, 3)
```
```

This begins with a set that has the values 1, 2, and 3. As with the List and Array types, Scala figures out that this is a Set[Int]. You can also see from the inferred type that by default we get an immutable set.

You can add to a set with +, you get back a new set that has the element after the plus sign added in. The second statement gives us back a set that includes 4 in addition to the 1, 2, and 3. In the third command we add a 2 to this new set. The result looks the same as the set before the 2 was added. This is because the set can not contain duplicate elements.

The last statement adds the value -10 into the set from res1. This value goes into the resulting set because there had not been a -10 previously. However, the result shows that order is not preserved in sets. Adding the -10 into the set not only put it in an odd place at the beginning, it also altered the location of the 4 in the set. From this you can see that you want to use sets when what you care about is the uniqueness of elements, not the order in which you get them.

The fact that the order can change means that "indexing" into a set in the manner we have done with an Array or a List do not have much meaning. You can perform that type of operation on a Set, but the meaning is a bit different. Consider the following examples.

```
```
scala> res3(2)
res4: Boolean = true

scala> res3(5)
res5: Boolean = false
```
```

¹ If you happen to be using a SortedSet, then the order of the objects will match the natural ordering of the type, but this is more the exception than the rule.