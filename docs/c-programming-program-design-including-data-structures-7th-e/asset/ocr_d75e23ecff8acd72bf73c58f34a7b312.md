which is the last element of the array `intArray`, into the container `vecList`. (Note that here, `first1` is `intArray`, `last` is `intArray + 9`, and `first2` is `vecList.begin()`.)
After the previous statement executes:

```
vecList = {5, 6, 8, 3, 40, 36, 98, 29, 75}
```

Next, consider the statement:

```
copy(intArray + 1, intArray + 9, intArray);
```

Here, `first1` is `intArray + 1`; that is, `first1` points to the location of the second element of the array `intArray`, and `last` is `intArray + 9`. Also, `first2` is `intArray`; that is, `first2` points to the location of the first element of the array `intArray`. Therefore, the second array element is copied into the first array component, the third array element into the second array component, and so on. After the preceding statement executes:

```
intArray = {6, 8, 3, 40, 36, 98, 29, 75, 75}
```

Clearly, the elements of the array `intArray` are shifted to the left by one position.

Now consider the statement:

```
copy(vecList.rbegin() + 2, vecList.rend(), vecList.rbegin());
```

Recall that the function `rbegin` (reverse begin) returns a pointer to the last element into a container; it is used to process the elements of a container in reverse. Therefore, `vecList.rbegin() + 2` returns a pointer to the third-to-last element into the container `vecList`. Similarly, the function `rend` (reverse end) returns a pointer to the first element into a container. The previous statement shifts the elements of the container `vecList` to the right by two positions. After the previous statement executes, the container `vecList` is:

```
vecList = {5, 6, 5, 6, 8, 3, 40, 36, 98}
```

Example 21-5 shows the effect of the preceding statements using a C++ program. Before discussing Example 21-5, let us describe a special type of iterators called **ostream iterators**. These iterators work well with the function `copy` to copy the elements of a container to an output stream.

# THE ostream ITERATOR AND THE FUNCTION copy

One way to output the contents of a container is to use a `for` loop, the function `begin` to initialize the `for` loop control variable, and the function `end` to set the limit. Alternatively, the function `copy` can be used to output the elements of a container. In this case, an iterator of type ostream specifies the destination. (ostream iterators are discussed in detail later in this chapter.) When we create an iterator of type ostream, we also specify the type of element that the iterator will output.

The following statement illustrates how to create an ostream iterator of type int:

```
ostream_iterator<int> screen(cout, " ");     //Line A
```