to move the elements of intList4 to the beginning of intList3. After the splice operation, intList4 is empty. The statement in Line 45 sorts intList3, and the statement in Line 49 merges intList2 and intList3 into intList2. After the merge operation, intList3 is empty. The meanings of the remaining statements are similar.

Examples 21-5 through 21-7 further clarify that iterators are important to efficiently process the elements of a container. Before describing associative containers, let us discuss iterators in some detail.

# Iterators

Iterators are similar to pointers. In general, an iterator points to the elements of a container (sequence or associative). Thus, with the help of iterators, we can successively access each element of a container.

The two most common operations on iterators are ++ (the increment operator) and * (the dereferencing operator). Suppose that cntItr is an iterator into a container. The statement:

```
++cntItr;
```

advances cntItr so that it points to the next element in the container. Similarly, the statement:

```
*cntItr;
```

gives access to the element of the container pointed to by cntItr.

# Types of Iterators

There are five types of iterators:

+   - Input iterators
+   - Output iterators
+   - Forward iterators
+   - Bidirectional iterators
+   - Random access iterators

The following sections describe these iterators.

# INPUT ITERATORS

Input iterators, with read access, step forward element by element; consequently, they return the values element by element. These iterators are provided for reading data from an input stream.

Suppose inputIterator is an input iterator. Table 21-11 describes the operations on inputIterator.