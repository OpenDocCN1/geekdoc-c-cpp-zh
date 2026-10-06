# Arrays and Lists in Scala

- nonEmpty – The opposite of isEmpty

```
scala> lst1.nonEmpty
res46: Boolean = true
```

```
scala> lst1.startsWith(List(7,5,6))
res47: Boolean = false
```

```
scala> lst1.startsWith(List(7,4,6))
res48: Boolean = true
```

+   - Search for something

+   - indexOf(elem:A) – Takes an element and returns the index of the first element in the collection to the value passed in. Gives back -1 if no matching element is found.

```
scala> lst1.indexOf(3)
res49: Int = 3
```

```
scala> lst1.indexOf(8)
res50: Int = -1
```

+   - lastIndexOf(elem:A) – Takes an element and returns the index of the last element in the collection to the value passed in. Gives back -1 if no matching element is found.

```
scala> lst1.lastIndexOf(4)
res51: Int = 1
```

+   - Other methods of note

+   - diff(that:Seq[A]) – Takes an argument that is a sequence of the same type as this is called and produces the multiset difference between the two. This means it will give you back all the elements that were in the original collection that do not have a match in the collection.

```
scala> lst1.diff(List(1,2,3,4))
res52: List[Int] = List(7, 6, 9)
```

```
scala> lst1.diff(Array(4,5,6))
res53: List[Int] = List(7, 3, 9, 1)
```

+   - distinct – Takes no arguments and produces a new collection that only contains the unique members of this collection, all duplicates are removed from the collection.

```
scala> List(1,2,3,8,5,1,2,8,2).distinct
res54: List[Int] = List(1, 2, 3, 8, 5)
```