in memory. The following shows how we can use member functions to insert new elements into a vector. Note that the last example copies the elements from the first to the next-to-last element.

```
vec.push_back(value);                  // Insert value at the back
vec.insert(pos, value);                 // Insert value before pos
vec.insert(pos, n, value);              // Insert n copies of value before pos
vec.insert(pos, first, last);           // Insert elements [first, last) before pos
```

The *pos* parameter is the position pointed to by the defined iterator. The *first* and *last* parameters are input iterators that define the range [first, last). They can be used to copy the elements in the host vector or another container.

**Erasure**  The vector class defines several member functions for erasure of one or more items in the container. Erasure at the back is very efficient and does not require reallocation of any items. An erasure from the middle or from the front requires reallocation of memory and should be avoided. The following shows the member functions we can use to erase elements from a vector.

```
vec.pop_back();                       // Erase the back (last) element
vec.erase(pos);                         // Erase the element before pos
vec.erase(first, second);               // Erase all the elements in the range [first, last)
vec.clear();                             // Erase all elements
```

# Application

The vector class is designed to look like an array. It has the same functionality as an array, but with some advantages. First, the vector is a class with built-in type operations. Second, it is allocated in the heap and can be resized as needed. Third, it has a well-defined iterator mechanism that allows us to access, insert, and erase elements. In summary, we can use a vector anytime we need an array and benefit from its advantages.

In Chapter 8 we learned how to use a two-dimensional array. We can do the same with a vector. We can create a two-dimensional vector, which is a vector of vectors. A vector of vectors has the same advantages over a two-dimensional array that a vector has over a one-dimensional array. In Program 19.3 we create a two-dimensional vector that simulates the multiplication table that is taught in elementary schools. To understand the instantiation, we show, step by step, how we code the definition of the two-dimensional vector.

```
vector <type> table(rows, value);
vector <vector <int> > table(rows, value);
vector <vector <int> > table(rows, vector <int>(cols));
```

In the first line, we define a vector named *table* of rows elements, each initialized to *value*. In the second line, we see that the type of the table is a vector of integers. In the third line, we see the value of each row is a vector of type integer and we have *cols* number of them. Note that a space between the two symbols (> >) is needed to show that the combination is not the >> operator.