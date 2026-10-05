# CHAPTER 10 Pointers and Dynamic Arrays

# EXAMPLE: A Class for Partially Filled Arrays

The class PFArrayD in Displays 10.10 and 10.11 is a class for a partially filled array of doubles. As shown in the demonstration program in Display 10.12, an object of the class PFArrayD can be accessed using the square brackets like an ordinary array, but it also automatically keeps track of how much of the array is used. Thus, it functions like a partially filled array. The member function getNumberUsed returns the number of array positions used and can be used in a for loop as in the following sample code:

```
PFArrayD stuff(cap); // cap is an int variable.
// some code to fill stuff with elements.
for (int index = 0; index < stuff.getNumberUsed(); index++)
    cout << stuff[index] << " ";
```

An object of class PFArrayD has a dynamic array as a member variable. This member variable stores the elements. The dynamic array variable is quite a pointer variable. In each constructor, this member variable is set to point at a dynamic array. There are also two member variables of type int: The member variable capacity records the size of the dynamic array, and the member variable used records the number of array positions that have been filled so far. As is customary with partially filled arrays, the elements must be filled in order, going first position 0, then 1, then 2, and so.

An object of the class PFArrayD can be used as a partially filled array of doubles. It has some advantages over an ordinary array of doubles or a dynamic array of doubles. Unlike the standard arrays, this array gives an error message if an illegal index is used. Also, an object of the class PFArrayD does not require an extra int variable to keep track of how much of the array is used. You may protest that "There is an int variable. It's a member variable." However, member is a private member variable in the implementation, and a programmer who uses the class PFArrayD need never be aware of that member variable.

An object of the class PFArrayD only works for storing values of type double. When we discuss templates in Chapter 16, you will see that it would be easy to convert the definition to a template that would work for any type, but for now we settle for storing elements of type double.

Most of the definition of the class PFArrayD use only items covered before now, but there are three new items: a copy constructor, a destructor, and an overloading of the assignment operator. We explain the overloaded operator next and discuss the copy constructor and destructor in the next two subsections.

> If you have already read the section of Chapter 7 on vectors, you will notice that the class defined here is a weak version of a vector. Even though you could use a vector any place that you would use this class, this is an instructive example using many of the techniques we discussed in this chapter. Moreover, this example will give you some insight into how a class might be implemented.