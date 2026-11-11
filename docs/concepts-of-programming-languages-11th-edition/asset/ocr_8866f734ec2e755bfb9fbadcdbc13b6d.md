# 8.3.4 Iteration Based on Data Structures

A general data-based iteration statement uses a user-defined data structure and a user-defined function (the iterator) to go through the structure's elements. The iterator is called at the beginning of each iteration, and each time it is called, the iterator returns an element from a particular data structure in some specific order. For example, suppose a program has a user-defined binary tree of data nodes, and the data in each node must be processed in some particular order. A user-defined iteration statement for the tree would successively set the loop variable to point to the nodes in the tree, one for each iteration. The initial execution of the user-defined iteration statement needs to issue a special call to the iterator to get the first tree element. The iterator must always remember which node it presented last so that it visits all nodes without visiting any node more than once. So an iterator must be history sensitive. A user-defined iteration statement terminates when the iterator fails to find more elements.

The for statement of the C-based languages, because of its great flexibility, can be used to simulate a user-defined iteration statement. Once again, suppose the nodes of a binary tree are to be processed. If the tree root is pointed to by a variable named root, and if traverse is a function that sets its parameter to point to the next element of a tree in the desired order, the following could be used:

```
```
for (ptr = root; ptr != null; ptr = traverse(ptr)) {
    . . .
}
```
```

In this statement, traverse is the iterator.

Predefined iterators are used to provide iterative access to PHP's unique arrays. The current pointer points at the element last accessed through iteration. The next iterator moves current to the next element in the array. The prev iterator moves current to the previous element. current can be set or reset to the array's first element with the reset operator. The following code displays all of the elements of an array of numbers $list:

```
```
reset $list;
print ("First number: " . current($list) . "");
while ($current_value = next($list))
    print ("Next number: " . $current_value . "<br />");
```
```

User-defined iteration statements are more important in object-oriented programming than they were in earlier software development paradigms, because users of object-oriented programming routinely use abstract data types for data structures, especially collections. In such cases, a user-defined iteration statement and its iterator must be provided by the author of the data abstraction because the representation of the objects of the type is not known to the user.

An enhanced version of the for statement was added to Java in Java 5.0. This statement simplifies iterating through the values in an array or objects