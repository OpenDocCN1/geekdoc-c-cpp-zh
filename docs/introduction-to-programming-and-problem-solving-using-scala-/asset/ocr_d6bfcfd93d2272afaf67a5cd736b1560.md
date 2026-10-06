# Arrays and Lists in Scala

# 6.3 Lists

Arrays are built in collection of choice in most non-functional languages. An Array is typically stored as a single block of memory. This makes them fast and efficient for a lot of operations. As we saw, Arrays are mutable. Functional languages tend to lean away from mutation and other side effects. If you do not allow mutation, Arrays becomes much efficient. If you want to change a single value in an immutable Array, you have to make a complete copy of the Array. For this reason, functional languages prefer to use lists. Technically the List type in Scala is an immutable singly linked lists, a data structure that you should become familiar with in a later course. You do not have to understand the structure in how to use it.

We can build a List using the syntax to build an Array with initial values.

```
scala List(7,4,6,3,9,1)
res15:List[Int] = List(7, 4, 6, 9, 1)
```

Like the Array, the List type is parametric and Scala will figure out the best type if you use this syntax.

Unlike Arrays, Lists do not have a fixed length determined at the time it is created. Then there is another way to put Lists together when we do not know initially all of the values that will be stored. We can easily build Lists one element at a time if we add to the front of the List. To add elements to a List we use the "cons" operator, :: Here is an example of adding a single element to an existing List.

```
scala val lst = List(2,3,4)
lst:List[Int] = List(2, 3, 4)
```

We begin by creating a List that contains 2, 3, and 4, then cons 1 to the beginning of the list. This operation did not alter the original List. It gave us a new list with an extra element at the beginning. Because of the way that Lists works, it is efficient. It did not have to copy the List to make it work. We can look at lst again to see that it has not changed.

```
scala lst
res17:List[Int] = List(2, 3, 4)
```

If you build a List with the cons operator, it is common to start with an empty List. There are two ways to represent an empty List in Scala. One is to not put arguments in the parentheses. The other is to use Nil. So we can build the same list we had before way.

```
scala 1::2::3::4::Nil
res18:List[Int] = List(1, 2, 3, 4)
```

You have to place the Nil at the end because the :: operator needs to have a List on the right hand side. Notice that for this to work, the :: operator is right associative.

> This was something we first discussed with the difference between val and var. As a general rule, programs are easier to reason about when they do not include mutation. Including mutation makes a number of things more complex by introducing new classes of errors.