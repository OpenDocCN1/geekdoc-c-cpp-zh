7. A Betelgeusean plorg has these properties:

# **Data**

A plorg has a name with no more than 19 letters.

A plorg has a contentment index (CI), which is an integer.

# **Operations**

A new plorg starts out with a name and a CI of 50.

A plorg's CI can change.

A plorg can report its name and CI.

The default plorg has the name "Plorga".

Write a `Plorg` class declaration (including data members and member function prototypes) that represents a `plorg`.Write the function definitions for the member functions.Write a short program that demonstrates all the features of the `Plorg` class.

8. You can describe a simple list as follows:

+   - The simple list can hold zero or more items of some particular type.
+   - You can create an empty list.
+   - You can add items to the list.
+   - You can determine whether the list is empty.
+   - You can determine whether the list is full.
+   - You can visit each item in the list and perform some action on it.

As you can see, this list really is simple; it doesn't allow insertion or deletion, for example.

Design a `List` class to represent this abstract type.You should provide a `list.h` header file with the class declaration and a `list.cpp` file with the class method implementations.You should also create a short program that utilizes your design.

The main reason for keeping the list specification simple is to simplify this programming exercise.You can implement the list as an array or, if you're familiar with the data type, as a linked list.But the public interface should not depend on your choice.That is, the public interface should not have array indices, pointers to nodes, and so on.It should be expressed in the general concepts of creating a list, adding