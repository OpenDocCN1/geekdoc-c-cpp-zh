
# Object-Oriented Programming with C++

print(print(print(cout,s1),s2),s3);

However, the statement

cout<<s1<<s2<<s3;

Moreover, what will happen in case of templates? Let us consider a common global template function that calls the insertion operator embedded within it. If we want to utilize such a function by passing an object of the class String as a parameter, the insertion operator would automatically get passed on the object. If the insertion operator has not been overloaded for the class String, compile-time error will arise. The narration and examples on function templates, from the chapter on templates (Chapter 10), clarify this. The extraction operators are overloaded for similar reasons as the insertion operators. The problem with String::setString() function is that the client needs to load the string that it wants to store in an object of the class String in a buffer and then passes it to this function. The formal argument of this function is of the same type as the data member that is storing the string. Obviously, the buffer should also be of the same type. The problem with this function is that the buffer must be passed to the function and that array must have the same type as the data member in which that is stored. If types change, the type of the buffer also needs to change. This forces the client to change. But, if the extraction operator is overloaded for the class String, the following statement can be used instead of calls to String::setString() function:

```cpp
cout<<s1;
```

The responsibility of reading data is shifted to the object itself. The manner in which the data is stored in the object and any change therein will no longer affect the client.

The insertion and extraction operators are overloaded to achieve independence of the implementation (definitions of member functions) from the interface (prototypes of member functions).

## 8.2.7 Overloading new and delete operators

The new and the delete operators can be overloaded for specific classes. The behaviour of these operators can be altered by operands of specific class types.

If these operators are overloaded for a specific class, then the functions that overload them are called when the class type is passed as a parameter to these operators. Otherwise, the global new and delete operators are overloaded. For example, if the new operator has been overloaded for a class X but not for a class Y, then the statement

```cpp
* Xptr = new X;
```

will call the function that overloads the new operator of class X. But the statement

```cpp
* Yptr = new Y;
```

will call the global operator. It is interesting to note that user programs may not change if the functions to overload the new and the delete operators are inserted into a class or removed from it.

The syntax for overloading the new operator (for allocating memory for a single object) is as shown in Listing 8.39.

## Operator Overloading, Type Conversion, New Style Casts, and RTTI

**Listing 8.39** Syntax for functions that overload the new operator and allocate memory for a single object

```cpp
class <class_name>
public:
    static void * operator new(size_t); //function
    /*
    //prototype
    rest of the class
    */
};
void <class_name> :: operator new ( size_t size )
    //function definition
{
    /*
    definition of the function
    */
}
```

The syntax for overloading the new operator (for allocating memory for an array of objects) is given in Listing 8.40.

**Listing 8.40** Syntax for functions that overload the new operator and allocate memory for an array of objects

```cpp
class <class_name>
public:
    static void * operator new [](size_t); //function
    /*
    //prototype
    rest of the class
    */
};
void <class_name>::operator new [] ( size_t size )
    //function definition
{
    /*
    definition of the function
    */
}
```

The syntax for overloading the delete operator (for deallocating memory for a single object) is given in Listing 8.41.

**Listing 8.41** Syntax for functions that overload the delete operator and deallocate memory for a single object

```cpp
class <class_name>
public:
    static void operator delete(void *,size_t);
    //function prototype
    /*
/* rest of the class
 */
void <class_name>::operator delete (void * p, size_t size)
    //function definition
```

```cpp
/*
definition of the function
*/
```

The syntax for overloading the delete operator (deallocating memory for an array of objects) is given in Listing 8.42.

Listing 8.42 Syntax for functions that overload the delete operator and deallocate memory for an array of objects

```cpp
class <class_name>
    public:
        static void operator delete [] (void *, size_t);
        //function prototype
        /*
        rest of the class
        */
```

```cpp
/*
definition of the function
*/
void <class_name>::operator delete []void *, size_t size)
    //function definition
```

The operator new function and the delete operator function must be static. However, their prototypes may or not be prefixed with the static keyword. Either way, the compiler treats these functions as static (for reasons that are explained in this chapter).

The return type of the operator new function must be of type void *. The value returned by this function is the address of the memory block by calling the global new operator. The operator new function should take at least one formal argument of type size_t. The return type of the operator new function must be of type void *. The value returned by this function is the address of the memory block by calling the global new operator. The operator new function should take at least one formal argument of type size_t. The size_t argument handles the amount of memory to be allocated.
