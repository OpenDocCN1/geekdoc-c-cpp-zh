# C.2 Friend Access and Overloading <<

In C++, a class can provide additional access to its private and protected objects by declaring other functions and classes as friends. Declaring a nonmember function as a friend to a class allows that to access all of the private and protected members of the class. Let's look at an example in which we need to declare a function as a friend of our class.

The output stream operator << is used to output stream of data to either the display or a file. We commonly stream integers, floating-point numbers, and strings to the display or a file, using <<. Occasionally, you may have even streamed a pointer to the list to help with troubleshooting or just to see what happened. C++ has defined the output operator's action for each of those data types. Trying to stream a list to the list using these statements

```
LinkedList<string> myList;
```

```
cout << myList;
```

results in a syntax error because there is no << operation for the LinkedList class. Notice that the syntax of the previous statement differs from the syntax of previous binary operators we overloaded. The expression cout << myList is shorthand for

```
cout.operator<<(myList)
```

Thus, when we define << for our LinkedList class, we are actually overloading the operator<< in the stream class of class which is an instance. Therefore, we need to define an operation for << in a different manner than the way we overloaded primitives.

Before discussing how to overload the output stream, let's consider what our list should look like if it is displayed or written to a file. If our list contains the four items Ace, Jack, Queen, and King, can we display them on a single line

Ace Queen King with a position label:

or on multiple lines

+   1 Ace
2 Jack
3 Queen
4 King

For our example, let's choose the second form of output—we could use public methods to display the list in our format, but we would need to call getEntry() iterates through the list from the beginning--to display each item. It is more efficient to access the data directly. Thus, in defining << for our LinkedList class, we should declare the operator<< in the stream class to access the private and protected data of list.

We grant access by making the operator method of LinkedList class by placing the following two statements in the header file:

```
template<<class friendType>
friend friendType operator<<(ostream&osStream,
             const LinkedList<friendType>& friendItemType, &outputList);
```

The keyword friend indicates that this method has access to private and protected data members and methods of our class as well as that which are public. Notice that the method returns an ostream object and that the first parameter is an ostream object. This is because we are overloading an operator method from the ostream class. Also, since the operator is not part of the LinkedList class, we cannot use the same template Type in the declaration; we must declare another template type in our example.