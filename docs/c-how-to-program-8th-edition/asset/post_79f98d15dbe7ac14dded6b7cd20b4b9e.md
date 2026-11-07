
### Common Programming Error 11.4

> If the copy constructor simply copied the pointer in the source object to the target object's pointer, then both would point to the same dynamically allocated memory. The first destructor to execute would delete the dynamically allocated memory, and the other object's ptr would be undefined, a situation called a dangling pointer—this would likely result in a serious runtime error (such as early program termination) when the pointer was used.

### Array Destructor

Line 16 of Fig. 11.10 declares the class’s destructor (defined in Fig. 11.11, lines 36–39). The destructor is invoked when an object of class Array goes out of scope. The destructor uses delete [] to release the memory allocated dynamically by new in the constructor.

### Error-Prevention Tip 11.2

> If after deleting dynamically allocated memory, the pointer will continue to exist in memory, set the pointer’s value to 0 to indicate that the pointer no longer points to memory in the free store. By setting the pointer to 0, the program loses access to that free-store space, which could be reallocated for a different purpose. If you do not set the pointer to 0, your code could inadvertently access the reallocated memory, causing subtle, nonrepeatable logic errors.

### getSize Member Function

Line 17 of Fig. 11.10 declares function getSize (defined in Fig. 11.11, lines 42–45) that returns the number of elements in the Array.

### Overloaded Assignment Operator

Line 19 of Fig. 11.10 declares the overloaded assignment operator function for the class. When the compiler sees the expression integers1 = integers2 in line 46 of Fig. 11.9, the compiler invokes member function operator= with the call

```
integers1.operator=( integers2 )
```

Member function operator=’s implementation (Fig. 11.11, lines 49–67) tests for self-assignment (line 51) in which an Array object is being assigned to itself. When this is equal to the right operand’s address, a self-assignment is being attempted, so the assignment is skipped (i.e., the object is already itself; in a moment we’ll see why self-assignment is dangerous). If it isn’t a self-assignment, then the function determines whether the sizes of the two arrays are identical (line 55); in that case, the original array of integers in the left-side Array object is not reallocated. Otherwise, operator= uses delete (line 57) to release the memory originally allocated to the target array, copies the size of the source array to the size of the target array (line 58), uses new to allocate the memory for the target array and places the pointer returned by new into the array’s ptr member. Then the for statement in lines 62–63 copies the array elements from the source array to the target array. Regardless of whether this is a self-assignment, the member function returns the current object (i.e., *this in line 66) as a constant reference; this enables cascaded Array assignments such as x = y = z, but prevents ones like (x = y) = z because z cannot be assigned to the const Array reference that’s returned by (x = y). If self-assignment occurs, and function operator= did not test for this case, operator= would unnecessarily copy the elements of the Array into itself.

Then the const version of operator[] is required to execute a statement such as

```
cout << z[ 3 ] << endl;
```

Remember, a program can invoke only the const member functions of a const object.

Each definition of operator[] determines whether the subscript it receives as an argument is *in range*—if not, each throws an out_of_range exception. If the subscript is in range, the non-const version of operator[] returns the appropriate array element as a reference so that it may be used as a modifiable lvalue (e.g., on the left side of an assignment statement). If the subscript is in range, the const version of operator[] returns a copy of the appropriate element of the array. The returned character is an rvalue.

## 11.1.1 Operators as Member Functions vs. Non-Member Functions

Whether an operator function is implemented as a member function or as a non-member function, the operator is still used the same way in expressions. So which is best?

When an operator function is implemented as a member function, the leftmost (or only) operand must be an object (or a reference to an object) of the operator’s class. If the left operand must be an object of a different class or a fundamental type, this operator function must be implemented as a non-member function (as we did in Section 11.5 when overloading << and >> as the stream insertion and stream extraction operators, respectively). A non-member operator function can be made a friend of a class if that function must access private or protected members of that class directly.

Operator member functions of a specific class are called (implicitly by the compiler) only when the *left* operand of a binary operator is specifically an object of that class, or when the *single operand* of a unary operator is an object of that class.

### Commutative Operators

Another reason why you might choose a non-member function to overload an operator is to enable the operator to be *commutative*. For example, suppose we have a *fundamental type variable*, number, of type long int, and an *object* bigInteger1, of class HugeInteger (a class in which integers may be arbitrarily large rather than being limited by the machine word size of the underlying hardware; the class HugeInteger is developed in the chapter exercises). The addition operator (+) produces a *temporary* HugeInteger object as the sum of a HugeInteger and a long int (as in the expression bigInteger1 + number), or as the sum of a long int and a HugeInteger (as in the expression number + bigInteger1). Thus, we require the addition operator to be *commutative* (actually as it is with two fundamental-type operands). The problem is that the class object *must* appear on the *left* of the addition operator if that operator is to be overloaded as a member function. So, we also overload the operator as a non-member function to allow the HugeInteger to appear on the *right* of the addition. The operator+ function that deals with the HugeInteger on the left can still be a member function. The non-member function can simply swap its arguments and call the member function.

## 11.1.2 Converting between Types

Most programs process information of many types. Sometimes all the operations “stay within a type.” For example, adding an int to an int produces an int. It’s often necessary, however, to convert data of one type to data of another type. This can happen in assignments, in calculations, in passing values to functions and in returning values from functions. The compiler knows how to perform certain conversions among fundamental types. You can use *cast operators* to force conversions among fundamental types.

But what about user-defined types? The compiler cannot know in advance how to convert among user-defined types, and between user-defined types and fundamental types, so you must specify how to do this. Such conversions can be performed with conversion constructors—single-argument constructors that turn objects of other types (including fundamental types) into objects of a particular class.

A conversion operator (also called a *cast operator*) can be used to convert an object of one class into an object of another class or into an object of a fundamental type. Such a conversion operator must be a non-static member function. The function prototype

```
A::operator char *() const;
```

declares an *overloaded cast operator function* for converting an object of user-defined type A into a temporary char * object. The operator function is declared const because it does not modify the original object. An overloaded cast operator function does not specify a return type—the return type is the type to which the object is being converted. If s is a class object, when the compiler sees the expression `static_cast<char *>(s)`, the compiler generates the call

```
s.operator char *()
```

The operand s is the class object for which the member function operator char * is being invoked.

Overloaded cast operator functions can be defined to convert objects of user-defined types into fundamental types or into objects of other user-defined types. The prototypes

```
A::operator int() const;
A::operator OtherClass() const;
```

declare *overloaded cast operator functions* that can convert an object of user-defined type A into an integer or into an object of user-defined type OtherClass, respectively.

One of the nice features of cast operators and conversion constructors is that, when necessary, the compiler can call these functions implicitly to create temporary objects. For example, if an object s of a user-defined String class appears in a program at a location where an ordinary char * is expected, such as

```
cout << s;
```

the compiler can call the overloaded cast-operator function operator char * to convert the object into a char * and use the resulting char * in the expression. With this cast operator provided for a String class, the stream insertion operator does not have to be overloaded to output a String using cout.

![](img/bfd978e7e9b192bab46ec2a89e481263_517_0.png)

### Software Engineering Observation 11.6

> When a conversion constructor is used to perform an implicit conversion, C++ can apply only one implicit constructor call (i.e., a single user-defined conversion) to try to match the needs of another overloaded operator. The compiler will not satisfy an overloaded operator’s needs by performing a series of implicit, user-defined conversions.
