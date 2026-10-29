
# Display 16.4　Class Template Definition (part 2 of 2)

```cpp
template<class T>
Pair<T>::Pair(T firstValue, T secondValue)
{
    first = firstValue;
    second = secondValue;
}

template<class T>
void Pair<T>::setFirst(T newValue)
{
    first = newValue;
}

template<class T>
T Pair<T>::getFirst() const
{
    return first;
}
```

The member functions for a class template are defined the same way as member functions for ordinary classes. The only difference is that the member function definitions are themselves templates. For example, Display 16.4 shows appropriate definitions for the member functions setFirst and getFirst, and for the constructor with two arguments for the template class Pair. Notice that the class name before the scope resolution operator is Pair<T>, and not simply Pair. However, the constructor name after the scope resolution operator is the simple name Pair without any <T>.

The name of a class template may be used as the type for a function parameter. For example, the following is a possible function declaration for a function with a parameter for a pair of integers:

```cpp
int addUp(const Pair<int>& thePair);
//Returns the sum of the two integers in thePair.
```

Note that we specified the type—in this case, int—that is to be filled in for the type parameter T.

You can even use a class template within a function template. For example, rather than defining the specialized function addUp given in the preceding code, you could instead define a function template as follows so that the function applies to all kinds of numbers:

```cpp
template<class T>
T addUp(const Pair<T>& thePair);
//Precondition: The operator + is defined for values of type T.
//Returns the sum of the two values in thePair.
```

Almost all template class definitions have some restrictions on what types can reasonably be substituted for the type parameter (or parameters). Even a straightforward template class such as Pair does not work well with absolutely all types T. The type Pair<T> will not be well behaved unless the assignment operator and copy constructor are well behaved for the type T, since the assignment operator is used in member function definitions and since there are member functions with call-by-value parameters of type T. If T involves pointers and dynamic variables, then T should also have a suitable destructor. However, these are requirements you might expect a well-behaved class type T to have. So, these requirements are minimal. With other template classes, the requirements on the types that can be substituted for a type parameter may be more restrictive.

## Class Template Syntax

A class template definition and the definitions of its member functions are prefaced with the following:

```
template<class Type_Parameter>
```

The class and member function definitions are then the same as for any ordinary class, except that the Type_Parameter can be used in place of a type.

For example, the following is the beginning of a class template definition:

```
template<class T>
class Pair
{
public:
    Pair();
    Pair(T firstValue, T secondValue);
    ...
```

Member functions and overloaded operators are then defined as function templates. For example, the definition of the two-argument constructor for the preceding sample class template would begin as follows:

```
template<class T>
Pair<T>::Pair(T firstValue, T secondValue)
{
```

You can specialize a class template by giving a type argument to the class name, as in the following example:

```
Pair<int>
```

The specialized class name, like Pair<int>, can then be used just like any class name. It can be used to declare objects or to specify the type of a formal parameter.

## Type Definitions

You can define a new class type name that has the same meaning as a specialized class template name, such as Pair<int>. The syntax for such a defined class type name is as follows:

```
typedef Class_Name<Type_Argument> New_Type_Name;
```

For example,

```
typedef Pair<int> PairOfInt;
```

The type name PairOfInt can then be used to declare objects of type Pair<int>, as in the following example:

```
PairOfInt pair1, pair2;
```

The type name PairOfInt can also be used to specify the type of a formal parameter or used anyplace else a type name is allowed.

## Self-Test Exercises

- 9. Give the definition for the default (zero-argument) constructor for the class template Pair in Display 16.4.
- 10. Give the complete definition for the following function, which was discussed in the previous subsection:
  
  int addUp(const Pair<int>& thePair);
  //Returns the sum of the two integers in thePair.
- 11. Give the complete definition for the following template function, which was discussed in the previous subsection:
  
  template<class T>
  T addUp(const Pair<T>& thePair);
  //Precondition: The operator + is defined for values of type T.
  //Returns the sum of the two values in thePair

## EXAMPLE: **An Array Template Class**

In Chapter 10, we defined a class for a partially filled array of doubles (Displays 10.10 and 10.11). In this example, we convert that definition to a template class for a partially filled array of values of any type. The template class PFArray has a type parameter T for the base type of the array.

The conversion is routine. We just replace double (when it occurs as the base type of the array) with the type parameter T and convert both the class definition and the member function definitions to template form. The template class definition is given in Display 16.5. The member function template definitions are given in Display 16.6.

Note that we have placed the template definitions in a namespace. Namespaces are used with templates in the same way as they are used with simple, nontemplate definitions.

A sample application program is given in Display 16.7. Note that we have separated the class template interface, implementation, and application program into three files. Unfortunately, these files cannot be used for the traditional method of separate compilation. Most compilers do not yet accommodate such separate compilation. So, we do the best we can by #include-ing the interface and implementation files in the application file. To the compiler, that makes it look like everything is in one file.

## Display 16.5   Interface for the PFArray Template Class (part 1 of 2)

```cpp
//This is the header file pfarray.h. This is the interface for the class
//PFArray. Objects of this type are partially filled arrays with base
//type T.
#ifndef PFARRAY_H
#define PFARRAY_H

namespace PFArraySavitch
{
    template<class T>
    class PFArray
    {
    public:
        PFArray( ); //Initializes with a capacity of 50.

        PFArray(int capacityValue);

        PFArray(const PFArray<T>& pfaObject);

        void addElement(const T& element);
        //Precondition: The array is not full.
        //Postcondition: The element has been added.
```

## Display 16.5  Interface for the PFArray Template Class (part 2 of 2)

```
17    bool full( ) const;  //Returns true if the array is full;
                         //false, otherwise.

18    int getCapacity( ) const;

19    int getNumberUsed( ) const;

20    void emptyArray( );
      //Resets the number used to zero, effectively emptying the
      //array.

22    T& operator[](int index);
      //Read and change access to elements 0 through numberUsed - 1.

24    PFArray<T>& operator = (const PFArray<T>& rightSide);

25    virtual ~PFArray( );
private:
27    T* a; //for an array of T.
28    int capacity; //for the size of the array.
29    int used; //for the number of array positions currently in use.
30 };
31 }// PFArraySavitch
32 #endif // PFARRAY_H
```

## Display 16.6  Implementation for PFArray Template Class (part 1 of 3)

```cpp
//This is the implementation file pfarray.cpp.
//This is the implementation of the template class PFArray.
//The interface for the template class PFArray is in the file pfarray.h.

#include "pfarray.h"
#include <iostream>
using std::cout;

namespace PFArraySavitch
{
    template <class T>
    PFArray<T>::PFArray( ) : capacity(50), used(0)
    {
        a = new T[capacity];
    }
```

![](img/c76bba8c1d927f399768ffe2ab5f5bee_749_0.png)
