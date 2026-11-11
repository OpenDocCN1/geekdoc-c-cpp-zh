# CHAPTER 3:

# Data Structures

Python is based on three reference structures: tuples, lists, and dictionaries. These structures are actually objecting that may contain other objects. They have quite different utilities and allow you to store information of all types.

These structures have a number of common features:

To extract one or more objects from a structure, we always use the []

For numerically indexed structures (tuples and lists), the structures are indexed to 0 (the first position is position 0)

# The Tuples

This is a structure that groups multiple objects in indexed order. Its form is not modifiable (immutable) once created and is defined using parentheses. It has only one dimension. Any type of object can be stored in a tuple. For example, if you want to create a tuple with different objects, we use:

```
tup1 = (1, True, 7.5.9)
```

You can also create a tuple by using the tuple () function. Access to the values of a tuple is done by the classical indexing of structures. Thus, if we want to access the third element of our tuple, we use:

```
In []: tup1 [2]
```

```
Out []: 7.5
```

Tuples can be interesting because they require little memory. Else, on the other hand, they are used as outputs of functions returning several values. Tuples as structures are objects. They have methods that are clean. These are few for a tuple: