
The following creates a dynamically allocated variable of type Record and sets the member variables of the dynamic struct variable to 2001 and 'A':

```cpp
Record *p;
p = new Record;
p->number = 2001;
p->grade = 'A';
```

The notations `p->grade` and `(*p).grade` have the same meaning. However, the first is more convenient and is almost always the notation used.

## THE this POINTER

The this pointer is a predefined pointer that points to the calling object. For example, consider a class like the following:

```cpp
class Sample
{
public:
        ...
        void showStuff() const;
        ...
private:
        int stuff;
        ...
};
```

The following two ways of defining the member function showStuff are equivalent:

```cpp
void Sample::showStuff() const
{
    cout << stuff;
}

//Not good style, but this illustrates the this pointer:
void Sample::showStuff()
{
    cout << this->stuff;
}
```

Notice that this is not the name of the calling object, but is the name of a pointer that points to the calling object. The this pointer cannot have its value changed; it always points to the calling object.

As our earlier comment indicated, you normally have no need for the pointer this. However, in a few situations it is handy. One place where the this pointer is commonly used is in overloading the assignment operator, =, which we discuss next.

Since the this pointer points to the calling object, you cannot use this in the definition of any static member functions. A static member function normally has no calling object to which the pointer this can point.

## OVERLOADING THE ASSIGNMENT OPERATOR

In this book we usually use the assignment operator as if it were a void function. However, the predefined assignment operator returns a reference that allows for some specialized uses.

With the predefined assignment operator, you can chain assignment operators as follows: `a = b = c;`, which means `a = (b = c);`. The first operation, `b = c`, returns the new version of b. So, the action of `a = b = c;` is to set a as well as b equal to c. To ensure that your overloaded versions of the assignment operator can be used in this way, you need to define the assignment operator so it returns something of the same type as its left-hand side. As you will see shortly, the this pointer will allow you to do this. (No pun intended.) However, while this requires that the assignment operator return something of the type of its left-hand side, it does not require that it return a reference. Another use of the assignment operator explains why a reference is returned.

The reason that the predefined assignment operator returns a reference is so that you can invoke a member function with the value returned, as in `(a = b).f();` where f is a member function. If you want your overloaded versions of the assignment operator to allow for invoking member functions in this way, then you should have them return a reference. This is not a very compelling reason for returning a reference, since this is a pretty minor property that is seldom used. However, it is traditional to return a reference, and it is not significantly more difficult to return a reference than to simply return a value.

For example, consider the following class (which might be used for some specialized string handling that is not easily handled by the predefined class string):

```cpp
class StringClass
{
public:
    ...
    void someProcessing();
    ...
    StringClass& operator=(const StringClass& rtSide);
    ...
private:
    char *a;//Dynamic array for characters in the string
    int capacity;//size of dynamic array a
    int length;//Number of characters in a
};
```

As noted in Chapter 8, when you overload the assignment operator it must be a member of the class; it cannot be a friend of the class. That is why the above definition has only one parameter for operator=. For example, consider the following:

`s1 = s2;//s1 and s2 in the class StringClass`

In the above call, s1 is the calling object and s2 is the argument to the member operator =.

The following definition of the overloaded assignment operator can be used in chains of assignments like

`s1 = s2 = s3;`

and can be used to invoke member functions as follows:

`(s1 = s2).someProcessing();`

The definition of the overloaded assignment operator uses the this pointer to return the object on the left side of the = sign (which is the calling object):

```cpp
//This version does not work in all cases.
StringClass& StringClass::operator=(const StringClass& rtSide)
{
    capacity = rtSide.capacity;
    length = rtSide.length;
    delete [] a;
    a = new char[capacity];
    for (int i = 0; i < length; i++)
        a[i] = rtSide.a[i];
    return *this;
}
```

This version has a problem when used in an assignment with the same object on both sides of the assignment operator, like the following:

`s = s;`

When this assignment is executed, the following statement is executed:

`delete [] a;`

But the calling object is s, so this means

`delete [] s.a;`

The pointer s.a is then undefined. The assignment operator has corrupted the object s and this run of the program is probably ruined.

For many classes, the obvious definition for overloading the assignment operator does not work correctly when the same object is on both sides of the assignment operator. You should always check this case and be careful to write your definition of the overloaded assignment operator so that it also works in this case.

To avoid the problem we had with our first definition of the overloaded assignment operator, you can use the this pointer to test this special case as follows:

```cpp
//Final version with bug fixed:
StringClass& StringClass::operator=(const StringClass& rtSide)
{
    if (this == &rtSide)
    //if the right side is the same as the left side
    {
        return *this;
    }
    else
    {
        capacity = rtSide.capacity;
        length = rtSide.length;
        delete [] a;
        a = new char[capacity];
        for (int i = 0; i < length; i++)
            a[i] = rtSide.a[i];
        return *this;
    }
}
```

A complete example with an overloaded assignment operator is given in the next programming example.

### Example: A CLASS FOR PARTIALLY FILLED ARRAYS

The class PFArrayD in Displays 10.10 and 10.11 is a class for a partially filled array of doubles.⁵ As shown in the demonstration program in Display 10.12, an object of the class PFArrayD can be accessed using the square brackets just like an ordinary array, but the object also automatically keeps track of how much of the array is in use. Thus, it functions like a partially filled array. The member function getNumberUsed returns the number of array positions used and can thus be used in a for loop as in the following sample code:

```cpp
PFArrayD stuff(cap);//cap is an int variable.
<some code to fill object stuff with elements.>
for (int index = 0; index < stuff.getNumberUsed(); index++)
    cout << stuff[index] << " ";
```

An object of the class PFArrayD has a dynamic array as a member variable. This member variable array stores the elements. The dynamic array member variable is actually a pointer variable. In each constructor, this member variable is set to point at a dynamic array. There are also two member variables of type int: The member variable capacity records the size of the dynamic array, and the member variable used records the number of array positions that have been filled so far. As is customary with partially filled arrays, the elements must be filled in order, going first into position 0, then 1, then 2, and so forth.

An object of the class PFArrayD can be used as a partially filled array of doubles. It has some advantages over an ordinary array of doubles or a dynamic array of doubles. Unlike the standard arrays, this array gives an error message if an illegal array index is used. Also, an object of the class PFArrayD does not require an extra int variable to keep track of how much of the array is used. (You may protest that "There is such an int variable. It's a member variable." However, that member variable is a private member variable in the implementation, and a programmer who uses the class PFArrayD need never be aware of that member variable.)

An object of the class PFArrayD only works for storing values of type double. When we discuss templates in Chapter 16, you will see that it would be easy to convert the definition to a template class that would work for any type, but for now we will settle for storing elements of type double.

Most of the details in the definition of the class PFArrayD use only items covered before now, but there are three new items: a copy constructor, a destructor, and an overloading of the assignment operator. We explain the overloaded assignment operator next and discuss the copy constructor and destructor in the next two subsections.

To see why you want to overload the assignment operator, suppose that the overloading of the assignment operator were omitted from Displays 10.10 and 10.11. Suppose list1 and list2 are then declared as follows:

```cpp
PFArrayD list1(10), list2(20);
```

5 If you have already read the section of Chapter 7 on vectors, you will notice that the class defined here is a weak version of a vector. Even though you can use a vector anyplace that you would use this class, this is still an instructive example using many of the techniques we discussed in this chapter. Moreover, this example will give you some insight into how a vector class might be implemented.
