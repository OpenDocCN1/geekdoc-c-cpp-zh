The standard-library containers all know their number of elements and we can obtain it by calling size(). For example:

Click here to view code image

```
for (size_t i = 0; i<c.size(); ++i) size_t is the name of the type returned by a standard-library size()
c[] = 0;
```

However, rather traversing containers using indices from 0 to size(), the standard algorithms (Chapter 13) rely on the number of sequences delimited by pairs of iterators:

Click here to view code image

```
for (auto p = c.begin(); p!=c.end(); ++p)
*p = 0;
```

Here, c.begin() is an iterator pointing to the first element of c and c.end() points one-beyond-the-last element of c. Like pointers, iterators support ++ to move to the next element and * to access the value of the pointed-to element.

This begin() and end() are also used by the implementation of the range-for, so we can simplify loops over a range:

```
for (auto& x : c)
x=0;
```

Iterators are used to pass sequences to standard-library algorithms. For example:

```
sort(v.begin(),v.end());
```

This iterator model (§13.3) allows for great generality and efficiency. For details and more container operations, see Chapter 12 and Chapter 13.

The begin() and end() can also be defined as free-standing functions; §7.2. The versions of begin() and end() for const containers are called cbegin() and cend().

# 6.5.3 Iterators and “smart pointers”

User-defined iterators (§13.3) and “smart pointers” (§15.2.1) implement the operators and aspects of a pointer for their purpose and add offset as needed.

+   Access: * (for a class), and [] (for a container)
Iteration/navigation: ++ (forward), -- (backward), +=, =, +, and -
Copy and and/move:

# 6.5.4 Input and Output Operations

For pairs of integers, << means left-shift >> means right-shift. However, for iostreams, are the output and input operators, (§1.8, Chapter 11). For details and more I/O operations, see Chapter 11.

# 6.5.5 swap()