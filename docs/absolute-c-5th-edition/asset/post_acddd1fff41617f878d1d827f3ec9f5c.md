
# Classes, Pointers, and Dynamic Arrays

## EXAMPLE: (continued)

To see why you want to overload the assignment operator, suppose that the overloading of the assignment operator was omitted from Displays 10.10 and 10.11. Suppose list1 and list2 are declared as follows:

```
PFArrayD list1(10), list2(20);
```

If list2 has been given a list of numbers with invocations of list2.addElement, even though we are assuming there is no overloading of the assignment operator, the following assignment statement is still defined, but its meaning may not be what you would like it to:

```
list1 = list2;
```

With no overloading of the assignment operator, the default predefined assignment operator is used. As usual, this predefined version of the assignment operator copies the value of each member variables of list2 to the corresponding member variables of list1. The value of list1.a is changed to be the same as list2.a, and the value of list1.capacity is changed to be the same as list2.used. But this can cause problems.

The member list1.a contains a pointer, and the assignment statement sets this pointer to the same value as list2.a. Both list1.a and list2.a therefore point to the same place in memory. Thus, if you change the array list1.a, you will also change the array list2.a. Similarly, if you change the array list2.a, you will also change the array list1.a. This is not what we want. We want the assignment operator to produce a completely independent copy of the thing on the right-hand side. The way to fix this is to overload the assignment operator so that it does what we want it to do with objects of the class PFArrayD. This is what we have done in Displays 10.10 and 10.11.

The definition of the overloaded assignment operator in Display 10.11 is reproduced next:

```
PFArrayD& PFArrayD::operator=(const PFArrayD& rightSide)
{
    if (capacity != rightSide.capacity)
    {
        delete a;
        a = new double[rightSide.capacity];
    }

    capacity = rightSide.capacity;
    used = rightSide.used;
    for (int i = 0; i < used; i++)
        a[i] = rightSide.a[i];

    return *this;
}
```

(continued)

# CHAPTER 10 Pointers and Dynamic Arrays

## EXAMPLE: (continued)

When you overload the assignment operator it must be a member of the class; it cannot be a friend of the class. That is why the previous definition has only one parameter. For example, consider the following:

```
list1 = list2;
```

In the previous call, list1 is the calling object and list2 is the argument to the member operator =.
Notice that the capacities of the two objects are checked to see if they are equal. If they are not equal, then the array variable a of the left side (that is, of the calling object) is destroyed by using new. This ensures that the object on the left side of the assignment operator will have an array of the correct size, but also does something that is important: It ensures that if the same object occurs on both sides of the assignment operator, the array named by the member variable will not be deleted with a call to delete. To see why this is important, consider the following alternative and simpler definition of the overloaded assignment operator:

```
//This version has a bug:
PFArrayD& PFArrayD::operator=(const PFArrayD& rightSide)
{
    delete a;
    a = new double[rightSide.capacity];

    capacity = rightSide.capacity;
    used = rightSide.used;
    for (int i = 0; i < used; i++)
        a[i] = rightSide.a[i];

    return *this;
}
```

This version has a problem when used in an assignment with the same object on both sides of the assignment operator, like the following:

```
myList = myList;
```

When this assignment is executed, the first statement executed is

```
delete [] a;
```

But the calling object is myList, so this means the pointer myList.a is then undefined. The assignment operator has corrupted the object myList. This problem cannot happen with the definition of the overloaded assignment operator we gave in Display 10.11.

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_487_0.png)

# Shallow Copy and Deep Copy

When defining an overloaded assignment operator or a copy constructor, if your code simply copies the contents of member variables from one object to the other that is known as a shallow copy. The default assignment operator and the default copy constructor perform shallow copies. If there are no pointers or dynamically allocated data, this works fine. If member variable names a dynamic array (or points to some other dynamic structure), you normally do not want a shallow copy. Instead, you want to create a copy of what each member variable is pointing to, so that you create a separate and identical copy, as illustrated in Display 10.11. This is a deep copy and is what we normally do when overloading the assignment operator or defining a copy constructor.

# Destructors

Dynamically allocated variables have one problem: They do not go away unless your program makes a suitable call to delete. Even if the dynamic variable was created using a local pointer variable and the local pointer goes away.

# Destructor

The destructor of a class is a member function that is called automatically when an object of the class goes out of scope. Among things, this means that if an object of the class type is a local variable, then the destructor is called automatically before the function ends. Destructors are used to eliminate any allocated variables that have been created by the object so the memory occupied by these dynamic variables is returned to the manager. Destructors may perform up tasks as well. The name of a destructor must consist of the tilde symbol, ~, followed by the name of the class.

# Copy Constructors

A copy constructor is a constructor that has one parameter that is of the same type as the class. The one parameter must be a call-by-reference parameter, and normally the parameter is preceded by the const modifier, if it is a constant parameter. In all other respects a copy constructor is defined in the same way as any other constructor and can be used just like others. For example, if a program uses the PFArray defined in Display 10.10 might contain the following:

```
PFArray b(20);
for (int i = 0; i < 20; i++)
b.addElement(i);
PFArray temp(b); //Initialized by the copy constructor
```

The object b is initialized with the copy constructor that has a parameter of type const PFArray&. When used in this copy constructor is used just like any other constructor.

A copy constructor should be defined so that the object being initialized becomes a complete, independent of its argument. So, in the declaration

```
PFArray temp(b);
```

the member variable temp.a should not be set to the same value as b.a; that would produce two pointers pointing to the same dynamic array. The definition of the copy constructor is shown in Display 10.11. Note that in the definition of the constructor, a new dynamic array is created and the contents of one dynamic array are
