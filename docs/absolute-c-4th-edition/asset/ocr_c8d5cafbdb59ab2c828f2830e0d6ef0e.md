Note that the names *forward iterator*, *bidirectional iterator*, and *random-access iterator* refer to kinds of iterators, not type names. An actual type name would be something like `std::vector<int>::iterator`, which in this case happens to be a random-access iterator.

# KINDS OF ITERATOR

Different containers have different kinds of iterators. The following are the main kinds of iterators.

+   - *Forward iterators:* `++` works on the iterator.
+   - *Bidirectional iterators:* Both `++` and `--` work on the iterator.
+   - *Random-access iterators:* `++`, `--`, and random access all work with the iterator.

# Self-Test Exercises

4. Suppose the vector v contains the letters ’A’, ’B’, ’C’, and ’D’ in that order. What is the output of the following code?

```
using std::vector<char>::iterator;

iterator it = v.begin();
it++;
cout << *(i + 2) << " ";
it--;
cout << i[2] << " ";
cout << *(i + 2) << " ";
```

# CONSTANT AND MUTABLE ITERATORS

The categories of forward iterator, bidirectional iterator, and random-access iterator each subdivide into two categories—*constant* and *mutable*—depending on how the dereferencing operator behaves with the iterator. With a **constant iterator** the dereferencing operator produces a read-only version of the element. With a constant iterator p, you can use *p to assign it to a variable or output it to the screen, for example, but you cannot change the element in the container by, for example, assigning to *p. With a **mutable iterator** p, *p can be assigned a value, and that will change the corresponding element in the container. Phrased another way, with a mutable iterator p, *p returns an lvalue. The vector iterators are mutable, as shown by the following lines from Display 19.1:

```
cout << "Setting entries to 0;\n";
for (p = container.begin(); p != container.end(); p++)
    *p = 0;
```