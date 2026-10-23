# Tuple Zipped Type (Advanced)

Something that you need to do fairly frequently is to run through two collections at the same time, pulling items from the same location of each. One way to do this is to use the zip method to zip the collections together into a new collection of tuples. While this works well if you have two collections, especially if you use a for loop, it does not work as well for three or more collections, and it is fundamentally inefficient because the zip method will go through the effort of creating a real collection with a bunch of tuples in it.

To get around these limitations, the types for tuples of length 2 and 3 have a type associated with them called Zipped. The sole purpose of the Zipped type is to let you get the benefits of running through a zipped collection without actually doing the zipping. To get an instance of the Zipped type, simply make a tuple that has all the collections you want in it and call the zipped method. The Zipped type has some of the main higher-order methods that you are used to using on collections: exists, filter, flatMap, forall, foreach, and map. The difference is that in the Zipped type they take multiple arguments. Specifically, they take as many arguments as there are elements in the tuple. This is significant because if you call a function like map that is mapping a collection of tuples the function has to take one argument and go through some effort to pull the elements out of the tuple. With the Zipped type you do not have to do that as the function literals are supposed to take multiple arguments instead of a single tuple with the multiple values.

A comparison of the two approaches is shown here.

```
val l1=List(1,2,3)
val l2=List(4,5,6)
l1.zip(l2).map(t => t._1*t._2)
(l1,l2).zipped.map((v1,v2) => v1*v2)
```

For this example the first one is a bit shorter, but that typically will not be the case. More importantly, the first one relies on the _1 and _2 methods which will make the code hard to read and understand for anything with more logic. To get the benefit of easy to read names using zip you would have to do the following.

```
l1.zip(l2).map(t => {
  val (v1,v2)=t
  v1*v2
})
```

It remains an exercise for the reader to see what happens if you want to iterate over three collections using zip. Consider the Zipped type when you need to iterate over two or three collections at the same time.