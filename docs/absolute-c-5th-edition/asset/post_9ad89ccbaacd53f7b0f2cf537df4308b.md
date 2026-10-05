
# Nodes and Linked Lists 733

Sections 17.1 through 17.3 do not use the material in Chapters 13 through 15 (recursion, inheritance, and polymorphism), with one small exception: We have marked our class destructors with the modifier virtual following the advice in Chapter 15. If you have not yet read about virtual functions (Chapter 15), you can pretend that "virtual" does not appear in the code. For the purposes of this chapter, it makes no difference whether "virtual" is present or not. Section 17.4 uses recursion (Chapter 13) but does not use Chapters 14 and 15.

## 17.1 Nodes and Linked Lists

A linked list, like the one outlined in Display 17.1, is a simple example of a dynamic data structure. It is called a dynamic data structure because each of the boxes in Display 17.1 is a variable of a struct or class that has been dynamically created with the new operator. In a dynamic data structure, these boxes, known as nodes, contain pointers, drawn as arrows, that point to other nodes. This section introduces the basic techniques for building and maintaining linked lists.

## Nodes

A structure like the one shown in Display 17.1 consists of items that we have drawn as boxes connected by arrows. The boxes are called nodes. Each of the nodes in Display 17.1 contains a string value, an integer, and a pointer that can point to other nodes of the same type. Note that pointers point to the entire node, not the individual items (such as 10 or "rolls") that are inside the node.

Nodes are implemented in C++ as structs or classes. For example, the struct type definitions for a node of type shown in Display 17.1, along with the type definition for a pointer to such nodes, can be as follows:

```cpp
struct ListNode
{
    string item;
    int count;
    ListNode *link;
}
```

```cpp
typedef ListNode* ListNodePtr;
```

The order of type definitions is important. The definition of ListNode must come first, since it is used in the definition of ListNodePtr.

The box labeled head in Display 17.1 is not a node but a pointer variable that can point to a node. The pointer variable head is declared as follows:

```cpp
ListNode head;
```

734 CHAPTER 17 Linked Data Structures

Even though we have ordered the type definitions to avoid some illegal forms of circularity, the preceding definition of the type ListNode is still circular. The definition of the type ListNode uses the type name ListNode to define the member variable link. There is nothing wrong with this particular circularity, which is allowed in C++. One indication that this definition is not inconsistent with the fact that you can draw pictures, as Display 17.1, that represent such structures.

We now have pointers inside structs and these pointers pointing to structs that contain containers, and so forth. In such situations the syntax gets sometimes involved, but in all cases the syntax follows these few rules we have described for the situation. If it is diagrammed in Display 17.1, and you want to change the number in the first node from 10 to 12, one way to accomplish this is with the following statement:

```cpp
(*head).count = 12;
```

The expression on the left side of the assignment operator may require a bit of explanation. The expression head is a pointer variable. The expression head is thus the thing it points to, namely the node (dynamic variable) containing "rolls" and the integer 10. This node, referred to by *head, is a struct, and the member variable of this struct, which contains a value of type int, is called count; therefore, (*head).count is the name of the int variable in the first node. The parentheses around *head are not optional. You want the dereferencing operation, *, to be performed before the dot operation. However, the dot operator has higher precedence than the dereferencing

Display 17.1 Nodes and Pointers

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_763_0.png)

Nodes and Linked Lists

operator, *, and without the parentheses, the dot operation would be performed first (which would produce an error). The next paragraph describes a shortcut notation to avoid this worry about parentheses.

C++ has an operator that can be used with a pointer to simplify the notation for accessing the members of a struct or a class. Chapter 10 introduced the arrow operator (., but we have not used it extensively before. So, a review is in order.

The arrow operator combines the actions of a dereferencing operator, *, and a dot operator to specify a member of a dynamic struct or object that is pointed to by a given pointer. For example, the previous assignment statement for changing the first node can be written more simply:

```cpp
head->count = 12;
```

This assignment statement and the previous one mean the same thing, but this one is the form normally used.

The string in the first node can be changed from "rolls" to "bagels" with the following statement:

```cpp
head->item = "bagels";
```

The result of these changes to the first node in the list is diagrammed in Display 17.2.

## Display 17.2 Accessing Node Data

```cpp
head->count = 12;
head->item = "bagels";
```

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_764_0.png)

765 CHAPTER 17 Linked Data Structures

## The Arrow Operator

The arrow operator combines the actions of a dereferencing operator, *, and a dot operator to specify a member of a dynamic struct or object that is pointed to by a given pointer. For example, the previous assignment statement for changing the first node can be written more simply:

```cpp
head->count = 12;
```

This assignment statement and the previous one mean the same thing, but this one is the form normally used.

The string in the first node can be changed from "rolls" to "bagels" with the following statement:

```cpp
head->item = "bagels";
```

NULL is a special constant value that is used to give a value to a pointer variable that would otherwise have no value. NULL can be assigned to a pointer variable of any type. The identifier NULL is defined in a number of libraries, such as <iostream> and <cstddef>.

The constant NULL is actually the number 0, but we prefer to think of it and spell it as NULL to make clear it means no memory location. NULL is typically used for two different purposes: First, NULL is used to give a value to a pointer variable that would otherwise have no value. The second category of use is that of an end marker. A program can step through the list as shown in Display 17.2 and know when it has reached the end of the list. The definition of NULL is handled by the C++ preprocessor, which replaces NULL with 0. Thus, the compiler never sees "NULL", so are no namespace issues; therefore, no using directive is needed.

A pointer can be set to NULL using the assignment operator, as in the following, which declares a pointer variable and initializes it to NULL:

```cpp
double *there = NULL;
```

You should always keep one pointer variable pointing to the head of a linked list. This pointer variable is a way to name the linked list. When you write a function that takes a linked list as an argument, this pointer (which points to the head of the linked list) can be used as the linked list argument.

## Linked Lists as Arguments

You should always keep one pointer variable pointing to the head of a linked list. This pointer variable is a way to name the linked list. When you write a function that takes a linked list as an argument, this pointer (which points to the head of the linked list) can be used as the linked list argument.

766 Nodes and Linked Lists

## Self-Test Exercises

- 1. Suppose your program contains the following type definitions:

```cpp
struct Box
{
    string name;
    int number;
    Box *next;
};
typedef Box* BoxPtr;
```

What is the output produced by the following code?

```cpp
BoxPtr head;
head = new Box;
head->name = "Sally";
head->number = 18;
cout << (*head).name << endl;
cout << head->name << endl;
cout << (*head).number << endl;
cout << head->number << endl;
```
