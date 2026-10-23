# 7.4 Standard Methods

One of the strengths of Scala is that it has rich interfaces. These are interfaces with a lot of different methods in them. We looked at length and size on the Array and head and tail on the List, but this was only scratching the surface. You can actually call either of those on either Lists or Arrays. However, length and size are not that efficient for Lists while tail is inefficient on the array. In this section we will run through a sampling of the other methods that are available to us when working with Lists and Arrays. We will start with the simple ones.

# 7.4.1 Basic Methods

The methods are broken into a few groups based on what they do. Inside of each group the methods are in alphabetical order. The methods that say they give you a new collection return a collection of the same type that it is called on. So if you call them on an Array you will get back an Array. If you call them on a List you will get back a List. Short examples are shown for each using the lst variable defined above. The type Seq appears occasionally. You can think of this as an Array or a List.

+   - Methods that give you part of a collection

+   - drop(n:Int) – Takes an Int and gives you back a new collection with all the elements after skipping that many.
+   
+     lst.drop(2)
+     res0: List[Int] = List(6, 3, 9, 1)

+   - init – Takes no arguments and returns a new collection with all the elements except the last.
+   
+     scala> lst.init
+     res0: List[Int] = List(7, 4, 6, 3, 9)

+   - last – Takes no arguments and returns the last element in the collection.
+   
+     scala> lst.last
+     res0: Int = 1

+   - slice(from:Int, until:Int) – Takes two arguments which are both integer indexes. It returns a new collection with all the elements beginning with the index of the first argument and ending with the one before the index of the second value.
+   
+     scala> lst.slice(2,4)
+     res0: List[Int] = List(6, 3)