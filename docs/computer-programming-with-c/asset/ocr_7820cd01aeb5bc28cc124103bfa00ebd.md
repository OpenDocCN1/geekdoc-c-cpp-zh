![](bbox=[0.14, 0.1, 0.86, 0.35])

> **How do I make a choice between private, public and protected inheritance?**
> Selecting between private, public or protected inheritance depends upon the requirements of data hiding to be implemented in the child class. It is recommended to use public inheritance since it preserves the access rules defined by the parent even in the child class. The choice to select appropriate access level for inheritance is still left to the programmer

In this book, we will write all the inheritance programs using ‘public inheritance’ because it gives us maximum degree of reusability.

# ### 14.3 Access Specifiers in C++: Revisited

C++ supports following three types of access specifiers:

# #### Private access

A private member or a member function can only be accessed inside a class in which the member is defined. This means that when a member variable is defined as private, its value cannot be accessed from outside of the class; and when a member function is defined as private it cannot be invoked from anyplace outside of the class.

# #### Public access

The public members/member functions of a class can be accessed from inside as well as outside the class. Hence, the public members can be accessed from anyplace in the C++ program.

# #### Protected access

Protected members and member functions of a class can be accessed inside the class in which they are defined as well as in all the child classes of that class. The protected