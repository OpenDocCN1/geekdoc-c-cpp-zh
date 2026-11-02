
```cpp
86      return ptr[ subscript ]; // reference return
87   } // end function operator[]
88
89   // overloaded subscript operator for const Arrays
90   // const reference return creates an rvalue
91   int Array::operator[]( int subscript ) const
92   {
93      // check for subscript out-of-range error
94      if ( subscript < 0 || subscript >= size )
95         throw out_of_range( "Subscript out of range" );
96
97      return ptr[ subscript ]; // returns copy of this element
98   } // end function operator[]
99
100   // overloaded input operator for class Array;
101   // inputs values for entire Array
102   istream &operator>>( istream &input, Array &a )
103   {
104      for ( size_t i = 0; i < a.size; ++i )
105         input >> a.ptr[ i ];
106
107      return input; // enables cin >> x >> y;
108   } // end function
109
110   // overloaded output operator for class Array
111   ostream &operator<<( ostream &output, const Array &a )
112   {
113      // output private ptr-based array
114      for ( size_t i = 0; i < a.size; ++i )
115      {
116         output << setw( 12 ) << a.ptr[ i ];
117
118         if ( ( i + 1 ) % 4 == 0 ) // 4 numbers per row of output
119            output << endl;
120      } // end for
121
122      if ( a.size % 4 != 0 ) // end last line of output
123         output << endl;
124
125      return output; // enables cout << x << y;
126   } // end function operator<<
```

**Fig. 18.11** | Array class member- and friend-function definitions. (Part 3 of 3.)

### Overloading the Stream Insertion and Stream Extraction Operators as friends

Lines 10–11 of Fig. 18.10 declare the overloaded stream insertion operator and the overloaded stream extraction operator as friends of class Array. When the compiler sees an expression like `cout << arrayObject`, it invokes *non-member function operator<<* with the call

```cpp
operator<<( cout, arrayObject )
```

When the compiler sees an expression like `cin >> arrayObject`, it invokes *non-member function operator>>* with the call

```cpp
operator>>( cin, arrayObject )
```

> **Software Engineering Observation 18.3**
> 
> *The argument to a copy constructor should be a const reference to allow a const object to be copied.*

> **Common Programming Error 18.4**
> 
> *If the copy constructor simply copied the pointer in the source object to the target object's pointer, then both would point to the same dynamically allocated memory. The first destructor to execute would delete the dynamically allocated memory, and the other object's ptr would point to memory that's no longer allocated, a situation called a dangling pointer—this would likely result in a serious runtime error (such as early program termination) when the pointer was used.*

## Array Destructor

Line 16 of Fig. 18.10 declares the class's destructor (defined in Fig. 18.11, lines 31–34). The destructor is invoked when an object of class Array goes out of scope. The destructor uses delete [] to release the memory allocated dynamically by new in the constructor.

> **Error-Prevention Tip 18.3**
> 
> *If after deleting dynamically allocated memory, the pointer will continue to exist in memory, set the pointer's value to nullptr to indicate that the pointer no longer points to memory in the free store. By setting the pointer to nullptr, the program loses access to that free-store space, which could be reallocated for a different purpose. If you do not set the pointer to nullptr, your code could inadvertently access the reallocated memory, causing subtle, nonrepeatable logic errors. We did not set ptr to nullptr in line 33 of Fig. 18.11 because after the destructor executes, the Array object no longer exists in memory.*

## getSize Member Function

Line 17 of Fig. 18.10 declares function getSize (defined in Fig. 18.11, lines 37–40) that returns the number of elements in the Array.

## Overloaded Assignment Operator

Line 19 of Fig. 18.10 declares the overloaded assignment operator function for the class. When the compiler sees the expression integers1 = integers2 in line 47 of Fig. 18.9, the compiler invokes member function operator= with the call

```cpp
integers1.operator=( integers2 )
```

Member function operator='s implementation (Fig. 18.11, lines 44–62) tests for self-assignment (line 46) in which an Array object is being assigned to itself. When this is equal to the right operand's address, a self-assignment is being attempted, so the assignment is skipped (i.e., the object already is itself; in a moment we'll see why self-assignment is dangerous). If it isn't a self-assignment, then the function determines whether the sizes of the two Arrays are identical (line 50); in that case, the original array of integers in the left-side Array object is not reallocated. Otherwise, operator= uses delete [] (line 52) to release the memory originally allocated to the target Array, copies the size of the source Array to the size of the target Array (line 53), uses new to allocate the memory for the target Array and places the pointer returned by new into the Array's ptr member. Then the for statement in lines 57–58 copies the elements from the source Array to the target Array. Regardless of whether this is a self-assignment, the member function returns the current object (i.e., *this in line 61) as a constant reference; this enables cascaded Array assignments such as x = y = z, but prevents ones like (x = y) = z because z cannot be assigned to the const Array reference that's returned by (x = y). If self-assignment occurs, and function operator= did not test for this case, operator= would unnecessarily copy the elements of the Array into itself.

> **Software Engineering Observation 18.4**
> 
> A copy constructor, a destructor and an overloaded assignment operator are usually provided as a group for any class that uses dynamically allocated memory. With the addition of move semantics in C++11, other functions should also be provided, as we discuss in Chapter 24 of our book C++ How to Program, 9/e.

> **Common Programming Error 18.5**
> 
> Not providing a copy constructor and overloaded assignment operator for a class when objects of that class contain pointers to dynamically allocated memory is a potential logic error.

## C++11: Move Constructor and Move Assignment Operator

C++11 adds the notions of a move constructor and a move assignment operator. We discuss these new functions in Chapter 24, C++11: Additional Features, of our book C++ How to Program, 9/e.

## C++11: Deleting Unwanted Member Functions from Your Class

Prior to C++11, you could prevent class objects from being copied or assigned by declaring as private the class's copy constructor and overloaded assignment operator. As of C++11, you can simply delete these functions from your class. To do so in class Array, replace the prototypes in lines 15 and 19 of Fig. 18.10 with:

```cpp
Array( const Array & ) = delete;
const Array &operator=( const Array & ) = delete;
```

Though you can delete any member function, it's most commonly used with member functions that the compiler can auto-generate—the default constructor, copy constructor, assignment operator, and in C++11, the move constructor and move assignment operator.

## Overloaded Equality and Inequality Operators

Line 20 of Fig. 18.10 declares the overloaded equality operator (==) for the class. When the compiler sees the expression integers1 == integers2 in line 55 of Fig. 18.9, the compiler invokes member function operator== with the call

```cpp
integers1.operator==( integers2 )
```

code that must be written in the class. Also, the full function definition for operator!= is in the Array header. This allows the compiler to inline the definition of operator!=.

## Overloaded Subscript Operators

Lines 29 and 32 of Fig. 18.10 declare two overloaded subscript operators (defined in Fig. 18.11 in lines 80–87 and 91–98, respectively). When the compiler sees the expression integers1[5] (Fig. 18.9, line 59), it invokes the appropriate overloaded operator[] member function by generating the call

```cpp
integers1.operator[]( 5 )
```

The compiler creates a call to the const version of operator[] (Fig. 18.11, lines 91–98) when the subscript operator is used on a const Array object. For example, if you pass an Array to a function that receives the Array as a const Array & named z, then the const version of operator[] is required to execute a statement such as

```cpp
cout << z[ 3 ] << endl;
```

Remember, a program can invoke only the const member functions of a const object.

Each definition of operator[] determines whether the subscript it receives as an argument is in range—and if not, each throws an out_of_range exception. If the subscript is in range, the non-const version of operator[] returns the appropriate Array element as a reference so that it may be used as a modifiable lvalue (e.g., on the left side of an assignment statement). If the subscript is in range, the const version of operator[] returns a copy of the appropriate element of the Array.

## C++11: Managing Dynamically Allocated Memory with unique_ptr

In this case study, class Array's destructor used delete [] to return the dynamically allocated built-in array to the free store. As you recall, C++11 enables you to use unique_ptr to ensure that this dynamically allocated memory is deleted when the Array object goes out of scope. In Chapter 22, we introduce unique_ptr and show how to use it to manage dynamically allocated objects or dynamically allocated built-in arrays.

## C++11: Passing a List Initializer to a Constructor

You can initialize an array object with a comma-separated list of initializers in braces, as in

```cpp
array< int, 5 > n = { 32, 27, 64, 18, 95 };
```

C++11 actually allows any object to be initialized with a list initializer. In addition, the preceding statement can also be written without the =, as in

```cpp
array< int, 5 > n{ 32, 27, 64, 18, 95 };
```

C++11 also allows you to use list initializers when you declare objects of your own classes. For example, you can now provide an Array constructor that would enable the following declarations:

```cpp
Array integers = { 1, 2, 3, 4, 5 };
```

or

```cpp
Array integers{ 1, 2, 3, 4, 5 };
```

each of which creates an Array object with five elements containing the integers from 1 to 5.
