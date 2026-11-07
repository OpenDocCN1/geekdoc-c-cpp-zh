
- A dependent name (p. 796) is an identifier that depends on the value of a template parameter. Resolution of dependent names occurs when the template is instantiated.
- Non-dependent names (p. 796) are resolved at the point where the template is defined.

## Section 19.5 Queues

- A queue is similar to a supermarket checkout line—the first person in line is serviced first, and other customers enter the line at the end and wait to be serviced.
- Queue nodes are removed only from a queue’s head and are inserted only at its tail.
- A queue is referred to as a first-in, first-out (FIFO) data structure. The insert and remove operations are known as enqueue and dequeue (p. 799).

## Section 19.6 Trees

- Binary trees (p. 803) are trees whose nodes all contain two links (none, one or both of which may have the value `nullptr`).
- The root node (p. 803) is the first node in a tree.
- Each link in the root node refers to a child. The left child is the root node of the left subtree (p. 803), and the right child is the root node of the right subtree (p. 803).
- The children of a single node are called siblings (p. 803). A node with no children is called a leaf node (p. 803).
- A binary search tree (p. 803) (with no duplicate node values) has the characteristic that the values in any left subtree are less than the value in its parent node (p. 803), and the values in any right subtree are greater than the value in its parent node.
- A node can only be inserted as a leaf node in a binary search tree.
- An inorder traversal (p. 804) of a binary tree traverses the left subtree, processes the value in the root node then traverses the right subtree. The value in a node is not processed until the values in its left subtree are processed. An inorder traversal of a binary search tree processes the nodes in sorted order.
- A preorder traversal (p. 804) processes the value in the root node, traverses the left subtree, then traverses the right subtree. The value in each node is processed as the node is encountered.
- A postorder traversal (p. 804) traverses the left subtree, traverses the right subtree, then processes the root node’s value. The value in each node is not processed until the values in both subtrees are processed.
- The binary search tree helps eliminate duplicate data (p. 811). As the tree is being created, an attempt to insert a duplicate value will be recognized and the duplicate value may be discarded.
- The level-order traversal (p. 811) of a binary tree visits the nodes of the tree row by row, starting at the root node level. On each level of the tree, the nodes are visited from left to right.

## Self-Review Exercises

- 19.1 Fill in the blanks in each of the following:
  - a) A self-__________ class is used to form dynamic data structures that can grow and shrink at execution time.
  - b) The __________ operator is used to dynamically allocate memory and construct an object; this operator returns a pointer to the object.
  - c) A(n) __________ is a constrained version of a linked list in which nodes can be inserted and deleted only from the start of the list and node values are returned in last-in, first-out order.

**19.3** A queue data structure allows nodes to be removed only from the head of the queue and inserted only at the tail of the queue. A queue is referred to as a first-in, first-out (FIFO) data structure. A stack data structure allows nodes to be added to the stack and removed from the stack only at the top. A stack is referred to as a last-in, first-out (LIFO) data structure.

- **19.4**
  - a) Classes allow us to instantiate as many data structure objects of a certain type (i.e., class) as we wish.
  - b) Class templates enable us to instantiate related classes, each based on different type parameters—we can then generate as many objects of each template class as we like.
  - c) Inheritance enables us to reuse code from a base class in a derived class, so that the derived-class data structure is also a base-class data structure (with public inheritance, that is).
  - d) Private inheritance enables us to reuse portions of the code from a base class to form a derived-class data structure; because the inheritance is private, all public base-class member functions become private in the derived class. This enables us to prevent clients of the derived-class data structure from accessing base-class member functions that do not apply to the derived class.
  - e) Composition enables us to reuse code by making a class object data structure a member of a composed class; if we make the class object a private member of the composed class, then the class object’s public member functions are not available through the composed object’s interface.

**19.5**

The inorder traversal is

`11 18 19 28 32 40 44 69 71 72 83 92 97 99`

The preorder traversal is

`49 28 18 11 19 40 32 44 83 71 69 72 97 92 99`

The postorder traversal is

`11 19 18 32 44 40 28 69 72 71 92 99 97 83 49`

## Exercises

- **19.6** (Concatenating Lists) Write a program that concatenates two linked list objects of characters. The program should include function `concatenate`, which takes references to both list objects as arguments and concatenates the second list to the first list.

- **19.7** (Merging Ordered Lists) Write a program that merges two ordered list objects of integers into a single ordered list object of integers. Function `merge` should receive references to each of the list objects to be merged and a reference to a list object into which the merged elements will be placed.

- **19.8** (Summing and Averaging Elements in a List) Write a program that inserts 25 random integers from 0 to 100 in order in a linked list object. The program should calculate the sum of the elements and the floating-point average of the elements.

- **19.9** (Copying a List in Reverse Order) Write a program that creates a linked list object of 10 characters and creates a second list object containing a copy of the first list, but in reverse order.

- **19.10** (Printing a Sentence in Reverse Order with a Stack) Write a program that inputs a line of text and uses a stack object to print the line reversed.

- **19.11** (Palindrome Testing with Stacks) Write a program that uses a stack object to determine if a string is a palindrome (i.e., the string is spelled identically backward and forward). The program should ignore spaces and punctuation.

### 19.12 (Infix-to-Postfix Conversion)

Stacks are used by compilers to help in the process of evaluating expressions and generating machine language code. In this and the next exercise, we investigate how compilers evaluate arithmetic expressions consisting only of constants, operators and parentheses.

Humans generally write expressions like 3 + 4 and 7 / 9 in which the operator (+ or / here) is written between its operands—this is called **infix notation**. Computers "prefer" **postfix notation** in which the operator is written to the right of its two operands. The preceding infix expressions would appear in postfix notation as 3 4 + and 7 9 /, respectively.

To evaluate a complex infix expression, a compiler would first convert the expression to postfix notation and evaluate the postfix version of the expression. Each of these algorithms requires only a single left-to-right pass of the expression. Each algorithm uses a stack object in support of its operation, and in each algorithm the stack is used for a different purpose.

In this exercise, you'll write a C++ version of the infix-to-postfix conversion algorithm. In the next exercise, you'll write a C++ version of the postfix expression evaluation algorithm. Later in the chapter, you'll discover that code you write in this exercise can help you implement a complete working compiler.

Write a program that converts an ordinary infix arithmetic expression (assume a valid expression is entered) with single-digit integers such as

```text
(6 + 2) * 5 - 8 / 4
```

to a postfix expression. The postfix version of the preceding infix expression is

```text
6 2 + 5 * 8 4 / -
```

The program should read the expression into string infix and use modified versions of the stack functions implemented in this chapter to help create the postfix expression in string postfix. The algorithm for creating a postfix expression is as follows:

1. Push a left parenthesis `(` onto the stack.
2. Append a right parenthesis `)` to the end of infix.
3. While the stack is not empty, read infix from left to right and do the following:
   - If the current character in infix is a digit, copy it to the next element of postfix.
   - If the current character in infix is a left parenthesis, push it onto the stack.
   - If the current character in infix is an operator,
     - Pop operators (if there are any) at the top of the stack while they have equal or higher precedence than the current operator, and insert the popped operators in postfix.
     - Push the current character in infix onto the stack.
   - If the current character in infix is a right parenthesis,
     - Pop operators from the top of the stack and insert them in postfix until a left parenthesis is at the top of the stack.
     - Pop (and discard) the left parenthesis from the stack.

The following arithmetic operations are allowed in an expression:

- `+` addition
- `-` subtraction
- `*` multiplication
- `/` division
- `^` exponentiation
- `%` modulus

[Note: We assume left-to-right associativity for all operators for the purpose of this exercise.] The stack should be maintained with stack nodes, each containing a data member and a pointer to the next stack node.

Some of the functional capabilities you may want to provide are:

- a) function `convertToPostfix` that converts the infix expression to postfix notation
