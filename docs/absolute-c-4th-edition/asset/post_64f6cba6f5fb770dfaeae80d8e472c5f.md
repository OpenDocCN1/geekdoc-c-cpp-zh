
# TYPE DEFINITIONS

You can define a new class type name that has the same meaning as a specialized class template name, such as Pair<int>. The syntax for such a defined class type name is as follows:

```
typedef Class_Name<Type_Arguments> New_Type_Name;
```

For example:

```
typedef Pair<int> PairOfInt;
```

The type name PairOfInt can then be used to declare objects of type Pair<int>, as in the following example:

```
PairOfInt pair1, pair2;
```

The type name PairOfInt can also be used to specify the type of a formal parameter or used anyplace else a type name is allowed.

## Self-Test Exercises

9. Give the definition for the default (zero-argument) constructor for the class template Pair in Display 16.4.

10. Give the complete definition for the following function, which was discussed in the previous subsection:

```
int addUp(const Pair<int>& thePair);
//Returns the sum of the two integers in thePair.
```

11. Give the complete definition for the following template function, which was discussed in the previous subsection:

```
template<class T>
T addUp(const Pair<T>& thePair);
//Precondition: The operator + is defined for values of type T.
//Returns the sum of the two values in thePair
```

# Example

## AN ARRAY TEMPLATE CLASS

In Chapter 10 we defined a class for a partially filled array of doubles (Displays 10.10 and 10.11). In this example, we convert that definition to a template class for a partially filled array of values of any type. The template class PFArray has a type parameter T for the base type of the array.

The conversion is routine. We just replace double (when it occurs as the base type of the array) with the type parameter T and convert both the class definition and the member function definitions to template form. The template class definition is given in Display 16.5. The member function template definitions are given in Display 16.6.

Note that we have placed the template definitions in a namespace. Namespaces are used with templates in the same way as they are used with simple, nontemplate definitions.

A sample application program is given in Display 16.7. Note that we have separated the class template interface, implementation, and application program into three files. Unfortunately, these files cannot be used for the traditional method of separate compilation. Most compilers do not yet accommodate such separate compilation. So, we do the best we can by #include-ing the interface and implementation files in the application file. To the compiler, that makes it look like everything is in one file.

## Display 16.5 Interface for the PFArray Template Class (part 1 of 2)

```
//This is the header file pfarray.h. This is the interface for the class
//PFArray. Objects of this type are partially filled arrays with base type T.
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

PFArray(const PFArray<T>& pfAobject);

void addElement(T element);
//Precondition: The array is not full.
//Postcondition: The element has been added.

bool full( ) const; //Returns true if the array is full; false, otherwise.

int getCapacity( ) const;

int getNumberUsed( ) const;

void emptyArray( );
//Resets the number used to zero, effectively emptying the array.
```

## Display 16.5 Interface for the PFArray Template Class (part 2 of 2)

```
T& operator[](int index);
//Read and change access to elements 0 through numberUsed - 1.

PFArray<T>& operator =(const PFArray<T>& rightSide);

virtual ~PFArray( );
private:
T *a; //for an array of T.
int capacity; //for the size of the array.
int used; //for the number of array positions currently in use.
};
}// PFArraySavitch
#endif //PFARRAY_H
```

## Display 16.6 Implementation for PFArray Template Class (part 1 of 3)

//This is the implementation file pfarray.cpp.
//This is the implementation of the template class PFArray.
//The interface for the template class PFArray is in the file pfarray.h.

```
#include "pfarray.h"
#include <iostream>
using std::cout;

namespace PFArraySavitch
{

template<class T>
PFArray<T>::PFArray() :capacity(50), used(0)
{
  a = new T[capacity];
}

template<class T>
PFArray<T>::PFArray(int size) :capacity(size), used(0)
{
  a = new T[capacity];
}

template<class T>
PFArray<T>::PFArray(const PFArray<T>& pfaObject)
  :capacity(pfaObject.getCapacity()), used(pfaObject.getNumberUsed())
{
  a = new T[capacity];
  for (int i = 0; i < used; i++)
    a[i] = pfaObject.a[i];
```

Note that the T is used before the scope resolution operator, but no T is used for the constructor name

## Display 16.6 Implementation for PFArray Template Class (part 2 of 3)

```
}

template<class T>
void PFArray<T>::addElement(T element)
{
    if (used >= capacity)
    {
        cout << "Attempt to exceed capacity in PFArray.\n";
        exit(0);
    }
    a[used] = element;
    used++;
}

template<class T>
bool PFArray<T>::full( ) const
{
    return (capacity == used);
}

template<class T>
int PFArray<T>::getCapacity( ) const
{
    return capacity;
}

template<class T>
int PFArray<T>::getNumberUsed( ) const
{
    return used;
}

template<class T>
void PFArray<T>::emptyArray( )
{
    used = 0;
}

template<class T>
T& PFArray<T>::operator[](int index)
{
    if (index >= used)
    {
        cout << "Illegal index in PFArray.\n";
        exit(0);
```

## Display 16.6 Implementation for PFArray Template Class (part 3 of 3)

```
}
       return a[index];
   }

   template<class T>
   PFArray<T>& PFArray<T>::operator =(const PFArray<T>& rightSide)
   {
       if (capacity != rightSide.capacity)
       {
           delete [] a;
           a = new T[rightSide.capacity];
       }
       capacity = rightSide.capacity;
       used = rightSide.used;
       for (int i = 0; i < used; i++)
           a[i] = rightSide.a[i];

       return *this;
   }

   template<class T>
   PFArray<T>::~PFArray()
   {
       delete [] a;
   }
   }// PFArraySavitch
```

## Display 16.7 Demonstration Program for Template Class PFArray (part 1 of 3)

```
//Program to demonstrate the template class PFArray.
#include <iostream>
#include <cstring>
using std::cin;
using std::cout;
using std::endl;
using std::string;

#include "pfarray.h"
#include "pfarray.cpp"
using PFArraySavitch::PFArray;

int main( )
{
```

![](img/9505fd46e120aa9c1406715936ff6251_668_0.png)

## Display 16.7 Demonstration Program for Template Class PFArray (part 3 of 3)

## SAMPLE DIALOGUE

Enter up to 10 nonnegative integers.
Place a negative number at the end.
1 2 3 4 5 -1
You entered the following:
1 2 3 4 5
Enter three words:
I love you
You wrote the following:
I love you
I hope you really mean it.

## FRIEND FUNCTIONS

Friend functions are used with template classes in the same way that they are used with ordinary classes. The only difference is that you must include a type parameter where appropriate.

## Self-Test Exercises

12. What do you have to do to make the following function a friend of the template class PFArray in Display 16.5?

```
void showData(PFArray<T> theObject);
//Displays the data in theObject to the screen.
//Assumes that << is defined for values of type T.
```

## THE vector AND basic_string TEMPLATES

If you have not yet done so, this would be a good time to read Section 7.3 of Chapter 7, which covers the template class vector.

Another predefined template class is the basic_string template class. The class basic_string is a template class that can deal with strings of elements of any type. The class basic_string<char> is the class for strings of characters. The class basic_string<double> is the class for strings of numbers of type double. The class basic_string<YourClass> is the class for strings of objects of the class YourClass (whatever that may be).
