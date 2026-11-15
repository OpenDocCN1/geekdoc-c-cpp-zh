
![](img/f2bfa570e453b020c16e048c79a3ea0e_541_0.png)

![](img/f2bfa570e453b020c16e048c79a3ea0e_541_1.png)

![](img/f2bfa570e453b020c16e048c79a3ea0e_541_2.png)

Figure 10.4 Binary tree with 5 nodes.

## The Node class

Since there is no built-in type to represent a node, we will define a new type to implement the concept of a node. A node in a binary tree is a type defined as a data value, a left child, and a right child. These three attributes are mutable so we will provide a public interface that includes three accessor methods and three mutator methods. A class diagram for a Node class is provided in Figure 10.6.

The class diagram in Figure 10.6 specifies an integer type for the data value of a Node. Note that the operations performed on a binary tree are independent of the type of the data value stored in each node. Thus, Node is a good candidate for a class template, where the type of the data value is the parameterized type. A class template for a generic node type will be developed after implementing and testing the data specific Node class.

| BinaryTree |
|---|
| - node* root |
| - void insert(node*, int) |
| - void print (ostream&, node*) const |
| - void clear (node*) |
| + void insert (int) |
| + void print (ostream&) const |
| + void clear() |
| + BinaryTree() |

Figure 10.5 UML BinaryTree class diagram.

| Node |
|---|
| - int data |
| - Node* left |
| - Node* right |
| + Node() |
| + Node(int) |
| + int getData() |
| + Node* getLeft() |
| + Node* getRight() |
| + int getData() |
| + void setLeft(Node*) |
| + void setRight(Node*) |
| + void setData(int) |

Figure 10.6 UML Node class diagram.

The implementation of the Node class described in Figure 10.6 is provided below. Notice the use of the preprocessor directives #ifndef, #define and #endif. These directives should be used in all header files to prevent the header file from being included more than once. If, for example, the header file Node.h is included in more than one file during compilation, the compiler will generate an error message similar to the one shown below.

![](img/f2bfa570e453b020c16e048c79a3ea0e_542_0.png)

```
error: redefinition of 'class Node'
```

This error is generated because the compiler is attempting to define the Node class for a second time. The preprocessor directive #ifndef is read “if not defined” and is followed by an identifier that is chosen, by convention, to be all uppercase letters and to reflect the name of the header file. The first time the header file is included, the preprocessor directive #ifndef returns true because the uppercase identifier has not yet been defined. Because #ifndef returns true, everything between #ifndef and #endif is processed, including the preprocessor directive #define NODE_H, which defines the identifier NODE_H. The next time the header file is included, the directive #ifdef NODE_H returns false; thus everything between #ifndef and #endif is ignored and a multiple of the Node class is avoided.

```
/*...............................................................*/
/* class declaration for node:                                 */
/* filename node.h                                             */
/*...............................................................*/

#ifndef NODE_H
#define NODE_H
class Node
{
  //Private attributes
  private:
    int data;
    Node *left;
    Node *right;

  //Public interface.
  public:
    Node();             //Default constructor
    Node(int);          //Parameterized constructor

    //Accessors
    Node* getLeft() const;
    Node* getRight() const;
    int getData() const;

    //Mutators
    void setLeft(Node*);
    void setRight(Node*);
    void setData(int v);
  };
#endif
```

```
/*...............................................................*/
/* Class implementation for node                               */
/* filename node.cpp                                           */
/*...............................................................*/

#include "node.h" //Required for Node.
using namespace std;

//Constructors.
Node::Node() : data(0), left(0), right(0)
{
}
```

```
Node::Node(int v) : data(v), left(0), right(0)
{
}
//Accessors
Node* Node::getLeft() const
{
    return left;
}
Node* Node::getRight() const
{
    return right;
}
int Node::getData() const
{
    return data;
}
```

```
//Mutators
void Node::setLeft(Node* l)
{
    left = l;
}
void Node::setRight(Node* r)
{
    right = r;
}
void Node::setData(int v)
{
    data = v;
}
/* ... */
```

To test the Node class, we will write a driver program that calls each of the methods at least once and prints the state of the attributes after each method is called.

```
/*
* Program chapter10_6 ........................
* This program tests the node class
* filename: nodeTest.cpp
*/
```

```
#include <iostream> //Required for cout.
#include "node.h" //Required for Node.
using namespace std;

int main() {
    Node n1, n3; //Test default constructor.
    Node n2(4); //Test parameterized constructor.

    //Test accessor methods.
    cout << "Value of n1 after default construction: "
         << endl << n1.getData() << " ," << n1.getLeft() << ","
         << n1.getRight() << endl;
```

```
cout << "Value of n2 after parameterized construction: "
<< endl << n2.getData() << " , " << n2.getLeft() << " , "
<< n2.getRight() << endl;
//Test mutator methods.
n1.setData(13);
n1.setLeft(n2);
n1.setRight(n3);
cout << "Value of n1 after modification: " << endl
<< n1.getData() << " , " << n1.getLeft() << " , "
<< n1.getRight() << endl;
cout << "Value of n2 after modification: " << endl
<< n2.getData() << " , " << n2.getLeft() << " , "
<< n2.getRight() << endl;
cout << "Value of n3 after modification: " << endl
<< n3.getData() << " , " << n3.getLeft() << " , "
<< n3.getRight() << endl;
return 0;
}
/*-------------------------------*/
```

A sample run of our test program generated the following output:

```
Value of n1 after default construction:
0 , 0 , 0
Value of n2 after parameterized construction:
4 , 0 , 0
Value of n1 after modification:
13 , 0xbffffaf0 , 0xbffffae4
Value of n2 after modification:
4 , 0 , 0
Value of n3 after modification:
0 , 0 , 0
```

## Practice!

Use the Node class developed in this section to answer the following questions. Consider the program given below:

```
#include <iostream>
#include "node.h"
using namespace std;
int main()
{
Node n1, n2(5);
cout << n1.getRight() << endl; //Line 1
cout << n2.getLeft() << endl; //Line 2
cout << n2.getData() << endl; //Line 3
n1.setLeft(&n2);
cout << n1.getLeft() << ' ' << n1.getRight()
     << ' ' << n1.getData() << endl; //Line 4
return 0;
}
```

- 1. Show the output generated by Line 1.
- 2. Show the output generated by Line 2.
- 3. Show the output generated by Line 3.
- 4. Show the output generated by Line 4.

## Recursive Member Functions

To continue the development of our BinaryTree class as diagramed in Figure 10.5, we must consider how we want to arrange the nodes in our tree and how we will traverse our binary tree. A binary tree may be ordered or unordered. An unordered binary tree assumes that there is no order imposed on the data values of the nodes that define the tree. An ordered binary tree imposes an ordering on the nodes of the tree.

### binary search tree

A binary search tree is an example of an ordered binary tree. A binary search tree is defined as a binary tree where:

- 1. each node has a value,
- 2. the left subtree of a node contains only nodes with values less than the node's value,
- 3. the right subtree of a node contains only nodes with values greater than or equal to the node's value.

A binary search tree with six nodes is displayed in Figure 10.7.

Binary search trees are popular data structures for storing large amounts of ordered data because of the speed with which a binary search tree can be traversed and modified. Notice in the diagram in Figure 10.7 that there is a unique path from the root of the tree to every other node in the tree. Notice also that each right child of a node and each left child of a node is the root of a smaller subtree. These two features allow for the development of efficient recursive algorithms for tree traversal.

### tree traversal

Traversing a tree refers to the process of visiting each node in a tree structure, exactly once, in a systematic way. Traversal algorithms are classified by the order in which the nodes are visited. For example, if we want the print() method to print the ordered data stored in the binary search tree represented in Figure 10.7, we would perform an in order traversal of the tree, printing the value of a node when it is visited. The recursive algorithm for an in order traversal of a tree is given below:
