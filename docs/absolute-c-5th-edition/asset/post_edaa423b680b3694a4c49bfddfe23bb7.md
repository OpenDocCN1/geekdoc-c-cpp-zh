
# 818 CHAPTER 17 Linked Data Structures

## MyProgrammingLab Programming Projects

Visit www.myprogramminglab.com to complete select exercises online and get instant feedback.

- 1. Write a void function that takes a linked list of integers and reverses the order of its nodes. The function will have call-by-reference parameter that is a pointer to the head of the list. After the function calls, this pointer will point to the head of a linked list that has the same nodes as the original list but in the reverse of the order they had in the original list. Note that your function will neither create or destroy any nodes. It will simply rearrange nodes. Place your function in a suitable test program.

- 2. Write a function mergelists takes two call-by-reference arguments that pointer variables to the heads of linked lists of values of type int. The two linked lists are assumed to be sorted so that the number at the head is the smallest, the number in the next node is the next smallest, and so forth. The function returns a pointer to the head of a new linked list that contains all the nodes in the original lists. The nodes in this longer list are also sorted from smallest to largest values. Note that your function will neither create or destroy any nodes. When the function ends, the two pointer variables arguments have the value NULL.

- 3. Design and implement a class that is a class for polynomials. The polynomial $a_nx^n + a_{n-1}x^{n-1} + \dots + a_0$ will be implemented as an int list. Each node will contain an int value for the power of x and for the corresponding coefficient. The class operations should include addition, subtraction, multiplication, and evaluation of a polynomial. Overload the operators +, -, and * for addition, subtraction, multiplication. Evaluation of a polynomial is implemented as a member function of type int. The evaluation member function returns the value obtained by plugging in an argument for x and performing the indicated operations.

Include four constructors: a default constructor, a copy constructor, with a single argument of type int that produces the polynomial that has only one constant term that is equal to the constructor argument, and a constructor with two arguments of type int that produces the one-term polynomial whose coefficient and exponent are given by the two arguments. (In the previous notation, the polynomial produced by the one-argument constructor is of the simple form consisting of only $a_0$. The polynomial produced by the two-argument constructor is of the slightly more complicated form $a_nx^n$.) Include member functions to input and output polynomials.

When the user inputs a polynomial, the user types in the following:

```
$a_nx^n + a_{n-1}x^{n-1} + \dots + a_0$
```

## Programming Projects

However, if a coefficient $a_j$ is 0, the user may omit the term $a_{x^j}$. For example, $3x^4 + 7x^2 + 5$ can be input as $3x^4 + 7x^2 + 5$.

 It could be input as $3x^4 + 0x^3 + 7x^2 + 0x^1 + 5$.

If a coefficient is negative, a minus sign is used in place of a plus sign, as in the following examples:

$3x^5 - 7x^3 + 2x^1 - 8$
$-7x^4 + 5x^2 + 9$

A minus sign at the front of the polynomial, as in the second of the previous examples, applies only to the first coefficient; it does not negate the entire polynomial. Polynomials are output in the same format. In the case of output, terms with 0 coefficients are not output. To simplify input, you can assume polynomials are always entered one per line and that there will always be a constant term $d_{ij}$. If there is no constant term, the user enters 0 for the constant term, as shown in the following:

$12x^8 - 3x^2 + 0$

- a. The annotation in Display 17.36 that a real SearchTree template class should have a copy constructor, an overloaded assignment operator, other overloaded operators, and member functions. Obtain the code for 17.36 and add declarations for the following functions and overloaded operators: default constructor, copy constructor, `delete`, overloaded operator, `=`, makeEmpty, height, size, `preOrderTraversal`, `inOrderTraversal`, `postOrderTraversal`. The functions `preOrderTraversal`, `inOrderTraversal`, `postOrderTraversal` each call a global function `process` nodes as they are encountered. The function `process` is a friend of the SearchTree class. For this exercise, it is only a stub. Supply conditions and postconditions for these functions describing what each function should do.

The function `height` has no parameters and returns the height of the tree. The height of the tree is the maximum of the heights of all the nodes. The height of a node is the number of links between it and the root node.

The function `size` has no parameters and returns the number of nodes in the tree.

The function `makeEmpty` removes all the nodes from the tree and returns the memory used by the nodes for reuse. The `makeEmpty` function leaves the root pointer with the value NULL.

- b. Implement the member and friend functions and overloaded operators. Note that some of the functions listed here are already implemented in the text. You should make full use of the text's code. You should test your package thoroughly.

- c. Design and implement an iterator class for the tree class. You will need to decide what a begin and end element means for your searchTree, and what will be the next element the ++ operator will point to.

Hint 1: You might maintain a private size variable that is increased by insertion and decreased by deletion, whose value is returned by the size function. An alternative (if you know calls to size are quite infrequent) to calculate the size when you need it by traversing the tree. Similar techniques, with more sophisticated details, can be used to implement the height function.

Hint 2: Do these few at a time. Compile and test after doing each of a few members. You will be glad you did this way.

Hint 3: Before you write the operator, =, and copy constructor, note that your jobs have a common task—duplicating another. Write a copyTree function that abstracts the common task of the copy constructor and operator,=. Then write two important functions using the common code.

Hint 4: The function isEmpty and the destructor have a common tree destruction task.

- 5. In an ancient land, the beautiful Eve had many suitors. She decided on the following to determine which position you would stand in to marry the princess if there are n suitors. Your program should simulate the elimination process by deleting the node that corresponds to each step. Be careful that you do not leave any leaks. Create a circular linked list of nodes to determine which position you would stand in to marry if there are n suitors. Starting at the first, the example follows:

1 suitor (priority 1)
2 suitor (priority 2)
3 suitor (priority 3)
4 suitor (priority 4)
5 suitor (priority 5)
6 suitor (priority 6)

Your program should create a circular linked list of nodes to determine which position you would stand in to marry the princess if there are n suitors. Your program should simulate the elimination process by deleting the node that corresponds to each step. Be careful that you do not leave any leaks.

- 6. Modify the queue class in Section 17.2 so that it implements a priority queue. A priority queue is similar to a regular queue except that each item added to the queue has an associated priority. For this problem, make the priority an integer where 0 is the highest priority and larger values are increasingly lower.

The remove function should return and remove the item that has the highest priority. For example:

```
q.add('X', 10);
q.add('Y', 1);
q.add('Z', 3);

cout << q.remove(); // Returns Y
cout << q.remove(); // Returns Z
cout << q.remove(); // Returns X
```

Test your queue with priorities in various orders (e.g., ascending, descending). You can implement the priority queue by performing a linear search in remove(). In future courses, you may study a data structure like a heap that affords a more efficient way to implement a priority queue.

- 7. Add a remove function, a cardinality function, and an iterator for the Set class given in Displays 17.28 and 17.29. Write a testable program.

- 8. The hash table from Displays 17.24 and 17.25 hashes a string to an integer and stores the same string in the hash table. Modify the hash table so that instead of storing strings it stores the combined first and last name, job title, and phone number. Use the Employee class so that it contains functions to get and set these member variables. Use the employee object as the input to the hash function. For most generality, you will also need to add a get function to the HashTable class that returns the Employee object stored in the hash that corresponds to the input name. The Employee class may require defining the == and != operators. Test your program by adding and retrieving several names, including names that have the same hash in the hash table.

- 9. Displays 17.24 through 17.26 provide the beginnings of a spell-checker. Refine the program to make it more useful. The modified program should read in a text file, parse each word, and determine whether each word is in the hash table and if not.
