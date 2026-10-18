Notice that we have overloaded the insertion operator << so it can be used to output an object of the class template GenericList. To do this, we made the operator << a friend of the class. In order to have a parameter that is of the same type as the class, we used the expression GenericList<ItemType> for the parameter type. When the type parameter is replaced by, for example, the type int, this list parameter will be of type GenericList<int>.

Also note that the implementation of the overloaded insertion operator << has been placed in the header file rather than the implementation file. This may seem unusual, but it is quite common when using friend functions or operators within a template. Although we are defining << like it is a member of GenericList, recall that friend functions really exist outside the class and are part of the namespace. The compiler will have an easy time finding the implementation of << this way when the class is included from other files.

A friend

# DISPLAY 17.4 Interface for the Class Template GenericList (part 1 of 2)

```
1  //This is the header file genericlist.h. This is the interface for the
2  //class GenericList. Objects of type GenericList can be a list of items
3  //of any type for which the operators << and = are defined.
4  //All the items on any one list must be of the same type. A list that
5  //can hold up to max items all of type Type_Name is declared as follows:
6  //GenericList<Type_Name> the_object(max);
7  #ifndef GENERICLIST_H
8  #define GENERICLIST_H
9  #include <iostream>
10 using namespace std;
11 
12 namespace listsavitch
13 {
14     template<class ItemType>
15     class GenericList
16     {
17     public:
18         GenericList(int max);
19         //Initializes the object to an empty list that can hold up to
20         //max items of type ItemType.
21         ~GenericList();
22         //Returns all the dynamic memory used by the object to the freestore.
23 
24         int length() const;
25         //Returns the number of items on the list.
26 
27         void add(ItemType newItem);
28         //Precondition: The list is not full.
29         //Postcondition: The newItem has been added to the list.
```

(continued)