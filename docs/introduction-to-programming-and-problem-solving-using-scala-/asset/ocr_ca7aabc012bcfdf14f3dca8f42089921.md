# 6.8.2 Summary of Concepts

+   - Arrays and Lists are collections that allow us to store multiple values under a single name. They are sequences, meaning that the values have an order and each one is associated with an integer index. Indexes start at zero.

+   - Both can be created in a number of ways.

+     - Array(e1,e2,e3,...) or List(e1,e2,e3,...) to make short collections where you provide all the values.
  - Use the : operator with Lists to append elements to the front and a new List. Use Nil to represent an empty List.
  - Array.fill(num)(byNameExpression) will make an Array of the specified size with values coming from repeated execution of the specified expression. This will also work for Lists.
  - Array.tabulate(num)(functionOnInt) will make an Array with num elements with values that come from evaluating the function and passing the index. Often function literals are used here. This will also work with List.

+   - Arrays have a fixed size and are mutable. Access and mutate using in parentheses: arr(i).

+   - Lists are completely immutable, but you can efficiently add to the front to make new Lists. They can be accessed with an index, but using head and tail in recursive functions is typically much more.

+   - The Scala collections, including Array and List, have lots of methods that you can call on to do things.
  - There are quite a few methods that take normal values for arguments and give you back values, parts of collections, of locations where things occurs.
  - The real power of collections is found in the higher-order methods. The primary ones you will use is map, filter, and foreach.
  - There are a handful of methods that give you back pieces of collections, including combinatorial possibilities as permutations and combinations.

# 6.8.3 Self-Directed Study

Enter the following statements into the REPL and see what they do. Try some variations to make sure you understand what is going on. Some of these are intended to fail. You should understand why.

```
scala> val arr = Array(1, 2, 3)
scala> arr(0)
scala> arr(1)
scala> arr(0) = 5
scala> arr.mkString(" ")
scala> val lst = List(2, 3, 5, 7, 11, 17)
scala> lst.head
scala> lst.tail
scala> val lst2 = 1 :: 2 :: 3 :: 4 :: 5 :: Nil
scala> lst.zip(lst2)
```