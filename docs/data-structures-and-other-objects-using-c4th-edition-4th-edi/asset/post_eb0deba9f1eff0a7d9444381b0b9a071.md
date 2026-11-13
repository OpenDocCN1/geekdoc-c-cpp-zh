
has been cached yet. Use a dynamic array of "checks," where each check is an object of a data type called check that you design and implement yourself. In addition to the checks, the program also reads all the deposits as well as the old and new account balance. You may want a second dynamic array to hold the list of deposits. The new account balance should equal the old balance plus all deposits, minus all checks that have been cashed.

The program also prints several items: the total of the checks cashed, the total of the deposits, what the new balance should be, and how much this figure differs from what the bank says the new account balance is. Also print two lists of checks: the checks cashed since the last time you balanced your checkbook, and a list of checks still not cashed.

Write a program that uses a dynamic list of strings to keep track of a list of chores that you have to accomplish today. The user of the program can request several services: (1) Add an item to the list of chores; (2) Ask how many chores are in the list; (3) Have the list of chores printed to the screen; (4) Delete an item from the list; (5) Exit the program. If you know how to program and write strings from a file, then have the program obtain its initial list of chores from a file. When the program ends, it should write all unfinished chores back to this file.

A common operation for input strings is to tokenize, or separate, strings with a delimiter of the user's choice. Write a string tokenizer function for a string class (either the one developed in this class, or the STL string). The function takes three parameters: a const string that contains the original input, a const string that designates the delimiter (for example, " "); and a container to store each token as it is found. Write a test program that prints out the tokens.

In this project, you will use the STL string class to manipulate an input string. Refer to Appendix H for various string functions that might be useful. Write an interactive program that prompts a user to input text of up to 10 lines. The input can be terminated with a special symbol(s), such as an asterisk, at the beginning of the final line. Give a second prompt to the user to enter a string of the form sub:replace, where sub is a substring of the original sentence and replace is a replacement string. The program should find each occurrence of sub and prompt the user for confirmation to replace the original text with the replacement string. Print the modified text after completion and prompt the user to exit or to enter another replacement string.

An array can be used to store large integers one digit at a time. For example, the integer 1234 could be stored in the array a by setting a[0] to 1, a[1] to 2, a[2] to 3, and a[3] to 4. However, for this project, you might find it easier to store the digits backward, that is, place 4 in a[0], place 3 in a[1], place 2 in a[2], and place 1 in a[3]. Design, implement, and test a class in which each object is a large integer with each digit stored in a separate element of an array. You'll also need a private member variable to keep track of the sign of the integer (perhaps a boolean variable). The number of digits may grow as the program runs, so the class must use a dynamic array. Discuss and implement other appropriate operators for this class.

Suppose that you want to implement a bag class to hold non-negative integers, and you never know that the biggest number in the bag will never be more than a few thousand. One approach for implementing this bag is to have a private member variable that is an array of integers called count with indexes from 0 to M (where M is the maximum number in the bag). If the bag contains six copies of a number n, then the object has count[n] = 6 to represent this fact. For this project, reimplement the bag class from Figure 4.9 using this idea. You will have an entirely new set of private member variables; for the public member functions, you may delete the reserve function, but please add a new function that the programmer can use to specify the maximum number that he or she anticipates putting into the bag. Also note that the insert member function must check to see whether the current maximum index of the dynamic array is at least as big as the new number. If not, then the array size must be increased.

## Chapter 5 Linked Lists

> The simplest way to interrelate or link a set of elements is to line them up in a single list... For, in this case only a single link is needed for each element to refer to its successor
>
> NIKLAUS WIRTH
> Algorithms + Data Structures = Programs

### Learning Objectives

- When you complete Chapter 5, you will be able to...
- design, implement, and test functions to manipulate nodes in a linked list, including inserting new nodes, removing nodes, searching for nodes, and processing (such as copying) that involves all the nodes of a list.
- design, implement, and test collection classes that use linked lists to store a collection of elements, generally using a node class to create and manipulate the linked lists.
- analyze problems that can be solved with linked lists and, when appropriate, propose alternatives to simple linked lists, such as doubly linked lists and lists with dummy nodes.
- understand the trade-offs between dynamic arrays and linked lists in order to correctly select between the STL vector, list, and deque classes

### Chapter Contents

- 5.1 A Fundamental Node Class for Linked Lists
- 5.2 A Linked-List Toolkit
- 5.3 The Bag Class with a Linked List
- 5.4 Programming Project: The Sequence Class with a Linked List
- 5.5 Dynamic Arrays vs. Linked Lists vs. Doubly Linked Lists
- 5.6 The STL Vector vs. the STL List vs. the STL Deque
- Chapter Summary
- Solutions to Self-Test Exercises
- Programming Projects

We begin this chapter with a concrete discussion of a new data structure, the linked list, which is used to implement a list of items arranged in some kind of order. The linked-list structure uses dynamic memory that shrinks and grows as needed, but in a different manner than dynamic arrays. The discussion of linked lists includes the necessary class definition in C++, together with fundamental functions to manipulate linked lists.

Once you understand the fundamentals, linked lists can be used as part of your container classes, similar to the way that arrays have been used in previous classes. For example, linked lists can be used to reimplement the bag and sequence classes from Chapter 3.

By the end of the chapter you will understand linked lists well enough to use them in various programming projects (such as the revised bag and sequence classes), and in the projects of future chapters. You will also know the advantages and drawbacks of using linked lists versus dynamic arrays for these projects.

### 5.1 A Fundamental Node Class for Linked Lists

A linked list is a sequence of items arranged one after another, with each item connected to the next by a link. A common programming technique is to place each item together with the link to the next item, resulting in a simple component called a node. A node is represented pictorially as a box with the item written inside the box and the link drawn as an arrow pointing out of the box.

Several typical nodes are drawn in Figure 5.1. For example, the topmost node has the number 12.1 as its data. Most of the nodes in the figure also have an arrow pointing out of the node. These arrows, or links, are used to connect one node to another. The links are represented as arrows because they do more than simply connect two nodes. The links also place the nodes in a sequence. In Figure 5.1, the five nodes form a sequence from top to bottom. The first node is linked to the second node, the second node is linked to the third node, and so on until we reach the last node. We must do something special when we reach the last node, since the last node is not linked to another node. In this special case, we replace the link in this node with a note saying “end marker.”

#### Declaring a Class for Nodes

As you might guess from our pictures, the links between nodes are implemented using pointers. But pointers to what? Remember that we cannot simply declare a

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_248_0.png)
