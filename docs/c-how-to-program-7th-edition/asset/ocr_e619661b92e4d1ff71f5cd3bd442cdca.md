# Using the Overloaded Subscript Operator

Line 58 uses the overloaded subscript operator to refer to integers1[5]—an in-range element of integers1. This subscripted name is used as an rvalue to print the value stored in integers1[5]. Line 62 uses integers1[5] as a modifiable lvalue on the left side of an assignment statement to assign a new value, 1000, to element 5 of integers1. We'll see that operator[] returns a reference to use as the modifiable lvalue after the operator confirms that 5 is a valid subscript for integers1.

Line 67 attempts to assign the value 1000 to integers1[15]—an out-of-range element. In this example, operator[] determines that the subscript is out of range, prints a message and terminates the program. We highlighted line 67 of the program in red to emphasize that it's an error to access an element that is out of range. This is a runtime logic error.

Interestingly, the array subscript operator [] is not restricted for use only with arrays; it also can be used, for example, to select elements from other kinds of container classes, such as linked lists, strings and dictionaries. Also, when operator[] functions are defined, subscripts no longer have to be integers—characters, strings, floats or even objects of user-defined classes also could be used. In Chapter 22, we discuss the STL map class that allows noninteger subscripts.

# Array Class Definition

Now that we've seen how this program operates, let's walk through the class header (Fig. 11.6). As we refer to each member function in the header, we discuss that function's implementation in Fig. 11.7. In Fig. 11.6, lines 34–35 represent the private data members of class Array. Each Array object consists of a size member indicating the number of elements in the Array and an int pointer—ptr—that points to the dynamically allocated pointer-based array of integers managed by the Array object.

# Overloading the Stream Insertion and Stream Extraction Operators as friends

Lines 11–12 of Fig. 11.6 declare the overloaded stream insertion operator and the overloaded stream extraction operator to be friends of class Array. When the compiler sees an expression like cout << arrayObject, it invokes global function operator<< with the call

```
```
operator<<( cout, arrayObject )
```
```

When the compiler sees an expression like cin >> arrayObject, it invokes global function operator>> with the call

```
```
operator>>( cin, arrayObject )
```
```

We note again that these stream insertion and stream extraction operator functions cannot be members of class Array, because the Array object is always mentioned on the right side of the stream insertion operator and the stream extraction operator. If these operator functions were to be members of class Array, the following awkward statements would have to be used to output and input an Array:

```
```
arrayObject << cout;
arrayObject >> cin;
```
```

Such statements would be confusing to most C++ programmers, who are familiar with cout and cin appearing as the left operands of << and >>, respectively.