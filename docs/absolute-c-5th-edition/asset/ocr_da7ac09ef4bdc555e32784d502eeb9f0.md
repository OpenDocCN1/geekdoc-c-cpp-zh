# Self-Test Exercises (continued)

10. Choose an ending to the following statement, and explain:

+   - For a large array and a list holding the same type objects, inserting a new object at a new location into the middle of a linked list compared to insertion in an array

+   - a. more efficient.
- b. less efficient.
- c. about the same.

11. Complete the body of the following function:

```
void insert (DoublyLinkedIntNode* afterMe, int theData);
```

The function should insert a new node with the value in theData after the node afterMe in a doubly linked list.

12. What operations are easier to implement with a doubly linked list than with a singly linked list? What operations are more difficult?

# EXAMPLE: A Generic Sorting Template Version of Linked List Tools

It is a routine matter to convert your type definitions and function definitions to templates that they will work for linked lists with data of any type T in the nodes. However, there are some details to worry about. The heart of what you need to do is replace the type of the data in a node (the node in Display 17.4) by a type parameter T and insert the following at the appropriate locations:

```
template<class T>
```

However, you should do a few more things to account for the fact that the T might be a class type. Since the type T might be a class type, a value parameter of type T should be changed to a constant reference parameter and a returned type of type T should be a const added so it is returned by constant value. (The reason for returning const is explained in Chapter 8.)

The final templates with the changes we described are shown in Displays 17.14 and 17.15. It was necessary to do one more change from the simple case of a linked list of integers. Since template typedefs are not implemented in some compilers, have not been able to use them. This means that on occasion we needed to use the following hard-to-read parameter type specification:

```
Node<T>**
```

(continued)