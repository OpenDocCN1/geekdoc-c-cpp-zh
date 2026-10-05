
# Answers to Self-Test Exercises

(or any other pointers), unless you are very aware of how it behaves on the pointers. The swapValues template function used with a type T is only as good, or as bad, as the assignment operator is on type T.

- 9. Since the type can be any type at all, there are no candidates for the default initialization values. So this constructor does nothing, but it does allow you to declare (uninitialized) objects without giving any constructor arguments.

```cpp
template<class T>
Pair<T>::Pair()
{
    //Do nothing.
}
```

- 10. int addUp(const Pair<int>& thePair)
{
    return (thePair.getFirst() + thePair.getSecond());
}

- 11. template<class T>
T addUp(const Pair<T>& thePair)
{
    return (thePair.getFirst() + thePair.getSecond());
}

- 12. Add the following to the public section of the template class definition of PFAArray:

```cpp
void showData(PFAArray<T> theObject);
//Displays the data in the object to the screen.
//Assumes << is defined for values of type T.
```

You also need to add a function template definition of showData. One possible definition is as follows:

```cpp
namespace PFAArraySavitch {
    template<class T>
    void showData(PFAArray<T> theObject) {
        for (int i = 0; i < theObject.used; i++)
            cout << theObject[i] << endl;
    }
}
```

- 13. Yes, it is perfectly legal. There are other, possibly preferable, ways to accomplish the same thing, but this is legal and not even crazy.

- 14. template<class T>
TwoDimPFAArrayBak<T>::TwoDimPFAArrayBak() 
    : PFAArray<T>()()

# 728 CHAPTER 16 Templates

## Programming Projects

Visit www.myprogramminglab.com to complete select exercises online and get instant feedback.

- 1. Write a template version of the iterative binary search algorithm from Display 13.8 which only searches an array of integers for an integer key. Specify requirements on the template parameter type. Discuss the requirements on the template parameter type.
- 2. Write a template version of the recursive binary search function from Display 13.6. Specify requirements on the template parameter type. Discuss the requirements on the template parameter type.
- 3. The template sort routine in Display 16.3 is based on an algorithm called the selection sort. Another related sorting algorithm is called insertion sort. The insertion sort algorithm is the method used to sort a Bridge. Each element in turn, inserting it into its proper place among the elements at the start of the array that are already sorted. The element being considered is inserted by moving the elements “the right” to make space and inserting the vacated place. For example, the following shows the steps in a selection sort of an array of ints a. The values of a [0] through [4] are given on each line. The asterisk marks the boundary between the sorted and unsorted portions of the array.

```
2 * 5 3 4
2 5 * 3 4
2 5 3 * 4
2 5 3 4 *
```

First, write an insertion sort function that works for ints. Next, write the template version of this sort function. Finally, test thoroughly using several primitive types, using a type with the minimal machinery necessary to use the sort routine.

- 4. Write a template-based function that calculates and returns the absolute value of two numeric values passed in. The function should operate with any numeric data (e.g., float, int, double, char).
- 5. Write a template-based class that implements a set of items. The class should allow the user to
   a. Add a new item to the set.
   b. Get the number of items in the set.
   c. Get a pointer to a dynamically created array containing each item in the set. The caller of this function is responsible for deallocating the memory.

Test your class by creating sets of different data types (e.g.

- 6. Do Programming Project 10.6 for the wrapper class around a dynamic array of strings that allowed for the deletion and addition of string entries. Except this time, use a template-based class so that the implementation is not limited to strings. Test the class with dynamic arrays of integers in addition to strings.

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_757_0.png)

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_758_0.png)

- 7. In this chapter, we used only a single template class type parameter. C++ allows you to specify multiple type parameters. For example, the following code specifies that the class accepts two type parameters:

```cpp
template
<class T, class V>
class Example
{
  ...
};
```

When creating an instance of the class, we must now specify two data types, such as Example<int, char> demo;

Modify the Pair class given in Display 16.4 so that the pair of items can be different data types. Write a main function that tests the class with pairs of different data types.

This page intentionally left blank

# Linked Data Structures 17

## 17.1 NODES AND LINKED LISTS 733

- Nodes 733
- Linked Lists 738
- Inserting a Node at the Head of a List 740
- Pitfall: Losing Nodes 743
- Inserting and Removing Nodes Inside a List 743
- Pitfall: Using the Assignment Operator with Data Structures- a Linked List 747
- Doubly Linked List 750
- Adding a Node to a Doubly Linked List 752
- Deleting a Node from a Doubly Linked List 752
- Example: A Generic Sorting Template Version of Linked List Tools 759

- Efficiency of Hash Tables 783
- Example: A Set Template Class 784
- Efficiency of Sets Using Linked Lists 790

## 17.3 ITERATORS 791

- Pointers as Iterators 792
- Iterator Classes 792
- Example: An Iterator Class 794

## 17.4 TREES 800

- Tree Properties 801
- Example: A Tree Class 803

## 17.2 LINKED LIST APPLICATIONS 763

- Example: A Stack Template Class 763
- Example: A Queue Template Class 770
- Tip: A Comment on Namespaces 773
- Friend Classes and Similar Alternatives 774
- Example: Hash Tables with Chaining 777

# 17 Data Structures

> If somebody had chanced to be
Who loved me in a manner true
> My heart would point him out to me
> And I would point him out to you.

GILBERT AND SULLIVAN, Ruddigore

# Introduction

A linked list is a list constructed using pointers. A linked list is not fixed in size but can grow and shrink while your program is running. A tree is another kind of data structure using pointers. This chapter introduces the use of pointers for building such structures, The Standard Template Library (STL) will predefined versions of these and other structures. The STL is covered in Chapter 19. It often makes sense to use the predefined data structures in the STL rather than defining your own. However, there are cases where you need to define your own structures using pointers. Also, this will give you some insight into how the STL might have been defined and will introduce you to some basic used material.

There are basically three ways to handle data structures of the kind discussed in this chapter:

- 1. The C-style approach of using global functions and structs with everything public own2. Using classes with all member variables private and using accessor and mutator functions
3. Using friend classes (or something similar, as private or protected inheritance or locally defined classes)

We give examples of all three methods. We introduce linked lists using method 1. We then present more details about basic linked lists and introduce both the stack and queue data structures using method 2. We give an alternate definition of our template class using friend classes (method 3), and also use friend classes (method 3) to present a tree template class. This way you can see the vertices and shortcomings of each approach. Our personal preference is to use friend classes, but each method has its own advocates.
