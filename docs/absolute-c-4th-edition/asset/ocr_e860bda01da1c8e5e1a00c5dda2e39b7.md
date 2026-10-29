The dereferencing operator *p always produces the element located at the iterator p. In some situations *p produces read-only access, which does not allow you to change the element. In other situations it gives you access to the element and will let you change the element. For vectors, *p will allow you to change the element located at p, as illustrated by the following for loop from Display 19.1:

```
for (p = container.begin(); p != container.end(); p++)
    *p = 0;
```

This for loop cycles through all the elements in the vector container and changes all the elements to 0.

# ITERATOR

An iterator is an object that can be used with a container to gain access to elements in the container. An iterator is a generalization of the notion of a pointer. The operators ==, !=, ++, and -- behave the same for iterators as they do for pointers. The basic outline of how an iterator can cycle through all the elements in a container is as follows:

```
iterator p;
for (p = container.begin(); p != container.end(); p++)
    Process_Element_At_location p;
```

The member function begin() returns an iterator located at the first element. The member function end() returns a value that serves as a sentinel value once an iteration past the last element in the container.

# DEREFERENCING

The dereferencing operator, *p, when applied to an iterator p, produces the element located at the iterator p. In some situations *p produces read-only access, which does not allow you to change the element. In other situations it gives you access to the element and will let you change the element.

# Self-Test Exercises

+   1. If v is a vector, what does v.begin() return? What does v.end() return?
+   2. If p is an iterator for a vector object v, what is *p?
+   3. Suppose v is a vector of ints. Write a for loop that will output all the elements of p except for the first element.