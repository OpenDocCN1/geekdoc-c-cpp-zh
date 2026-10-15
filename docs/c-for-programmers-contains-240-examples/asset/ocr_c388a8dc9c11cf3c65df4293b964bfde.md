```
15
16    i.setValue( 10 );
17
18    cout << "Interface contains: " << i.getValue()
19        << " after setValue" << endl;
20    return 0;
21 } // end main
```

Interface contains: 5 before setValue
Interface contains: 10 after setValue

Fig. 10.27 | Implementing a proxy class. (Part 2 of 2.)

# 10.11 Wrap-Up

In this chapter, we introduced several advanced topics related to classes and data abstraction. You learned how to specify const objects and const member functions to prevent modifications to objects, thus enforcing the principle of least privilege. You also learned that, through composition, a class can have objects of other classes as members. We introduced the topic of friendship and presented examples that demonstrate how to use friend functions.

You learned that the this pointer is passed as an implicit argument to each of a class’s non-static member functions, allowing the functions to access the correct object’s data members and other non-static member functions. You also saw explicit use of the this pointer to access the class’s members and to enable cascaded member-function calls.

We introduced the concept of dynamic memory management. You learned that you can create and destroy objects dynamically with the new and delete operators, respectively. We motivated the need for static data members and demonstrated how to declare and use static data members and static member functions in your own classes.

You learned about data abstraction and information hiding—two of the fundamental concepts of object-oriented programming. We discussed abstract data types—ways of representing real-world or conceptual notions to some satisfactory level of precision within a computer system. You then learned about three example abstract data types—arrays, strings and queues. We introduced the concept of a container class that holds a collection of objects, as well as the notion of an iterator class that walks through the elements of a container class. Finally, you learned how to create a proxy class to hide the implementation details (including the private data members) of a class from clients of the class.

In Chapter 11, we continue our study of classes and objects by showing how to enable C++’s operators to work with objects—a process called operator overloading. For example, you’ll see how to “overload” the << operator so it can be used to output a complete array without explicitly using a repetition statement.