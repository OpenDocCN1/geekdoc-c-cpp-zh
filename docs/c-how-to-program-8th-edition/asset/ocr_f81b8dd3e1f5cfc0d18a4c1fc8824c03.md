+   - Overloaded input and output operators are declared as friends if they need to access non-public class members directly for performance reasons.

# Section 11.6 Overloading Unary Operators

+   - A unary operator for a class can be overloaded as a non-static member function with no arguments or as a non-member function with one argument; that argument must be either an object of the class or a reference to an object of the class.

+   - Member functions that implement overloaded operators must be non-static so that they can access the non-static data in each object of the class.

# Section 11.7 Overloading the Unary Prefix and Postfix ++ and -- Operators

+   - The prefix and postfix increment and decrement operators can all be overloaded.

+   - To overload the pre- and post-increment operators, each overloaded operator function must have a distinct signature. The prefix versions are overloaded like any other unary operator. The postfix increment operator’s unique signature is accomplished by providing a second argument, which must be of type int. This argument is not supplied in the client code. It’s used implicitly by the compiler to distinguish between the prefix and postfix versions of the increment operator. The same syntax is used to differentiate between the prefix and postfix decrement operator functions.

# Section 11.9 Dynamic Memory Management

+   - Dynamic memory management (p. 469) enables you to control the allocation and deallocation of memory in a program for any built-int or user-defined type.

+   - The free store (sometimes called the heap; p. 469) is a region of memory assigned to each program for storing objects dynamically allocated at execution time.

+   - The new operator (p. 469) allocates storage of the proper size for an object, runs the object’s constructor and returns a pointer of the correct type. The new operator can be used to dynamically allocate (p. 469) any fundamental type (such as int or double) or class type. If new is unable to find space in memory for the object, it indicates that an error occurred by “throwing” an “exception.” This usually causes the program to terminate immediately, unless the exception is handled.

+   - To destroy a dynamically allocated object and free its space, use the delete operator (p. 469).

+   - An array of objects can be allocated dynamically with new as in

```
int *ptr = new int[100];
```

which allocates an array of 100 integers and assigns the starting location of the array to ptr. The preceding array of integers is deleted (p. 469) with the statement

```
delete [] ptr;
```

# Section 11.10 Case Study: Array Class

+   - A copy constructor initializes a new object of a class by copying the members of an existing one. Classes that contain dynamically allocated memory typically provide a copy constructor, a destructor and an overloaded assignment operator.

+   - The implementation of member function operator= should test for self-assignment (p. 481), in which an object is being assigned to itself.

+   - The compiler calls the const version of operator[] when the subscript operator is used on a const object and calls the non-const version of the operator when it’s used on a non-const object.

+   - The array subscript operator ([]) can be used to select elements from other types of containers. Also, with overloading, the index values no longer need to be integers.