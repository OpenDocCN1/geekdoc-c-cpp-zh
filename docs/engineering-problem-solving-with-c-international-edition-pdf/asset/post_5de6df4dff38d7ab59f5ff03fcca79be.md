
![](img/f2bfa570e453b020c16e048c79a3ea0e_547_0.png)

Figure 10.7 Binary search tree with 6 nodes.

```
inOrder traverse:
if(root == null)
    return
inOrder traverse left child
visit node
inOrder traverse right child
```

This algorithm begins at the root of a binary tree and calls itself recursively on the left child of each successive node until a null value is encountered. When a node with a null left child is eventually found, the node is “visited”, and the algorithm calls itself recursively on the right child of this node. The condition root == null is the terminating condition, and each recursive call reduces the problem to the traversal of a smaller subtree. Applying an in order traversal of the tree in Figure 10.7, and printing each nodes as it was visited would result in the following output: 8 10 14 19 22 27.

The algorithm for inserting a new node in the correct position to maintain the ordering of a binary search tree begins at the root of the tree. If the tree is empty, the new node is inserted as the first node in the tree. If the tree is not empty, the value of the new node is compared to the value of the first node. If the value of the new node is less than the root node, the algorithm calls itself on the left child, else the algorithm calls itself on the right child. The recursive algorithm is described below:

```
insert( node* root, int value ):
if(root == null)
    root = new node(value)
    return
else
if( value < root->value)
    insert(root->left child,value)
else
    insert(root->right child,value)
```

![](img/f2bfa570e453b020c16e048c79a3ea0e_548_0.png)

Figure 10.8 Binary search tree after insertion of a new node.

If the value 17 was inserted into the binary search tree in Figure 10.7, the resulting tree would look like the tree in Figure 10.8.

The algorithm for clearing a tree is described next.

```
clear(node* root):

if(root == null)
    return
else
    clear(root->left)
    clear(root->right)
    delete root
```

We can now complete the definition of the BinaryTree class as described in Figure 10.5.

```
/*................................................................*/
/* Binary tree declaration                                     */
/* filename: binaryTree.h                                      */
/*................................................................*/

#include "node.h" //Required for node.
#include <iostream> //Required for ostream.
using namespace std;

class BinaryTree {
public:
    //Default constructor.
    BinaryTree();
    
    //public. non recursive print and insert
    void print(ostream& out) const;
    void insert(int value);
    void clear();
private:
//private recursive overloaded print and insert
void print(ostream& out, node* rt) const;
void insert(node*& rt, int value);
void clear(node* rt);

//private attribute
Node* root;
};
/*................................................................*/
```

Notice in the declaration of the BinaryTree class that ......... print(), insert(), and clear() are overloaded. The public versions of these methods are not recursive. The private versions of these methods are recursive, and each has a formal parameter of type Node*.

The public versions of these methods must be called by a BinaryTree object, thus the root of the tree is provided by the calling object. The private versions of these methods calls themselves recursively, on the right and left subtree of the calling object, to traverse the tree. Thus the value of the formal parameter, rt, is different for each subsequent call and must be passed as an argument to support the recursive nature of these methods. The definition of a minimal BinaryTree class is given below:

```
/*...............................................................*/
/* Binary tree implementation                                  */
/* Filename: binaryTree.cpp                                    */
/*...............................................................*/

#include "BTree.h"    //Required for BinaryTree.
#include <iostream>   //Required for ostream.
using namespace std;

//Constructor
BinaryTree::BinaryTree():root(0)
{
}

//print: Public method
void BinaryTree::print(ostream& os) const
{
    if(root == NULL)
    {
        cout << "tree is empty ";
        return;
    }
    else
        print(os, root); //call private print()
}

//print: Private recursive method
void BinaryTree::print(ostream& os, node* theRoot) const
{
    if(theRoot == NULL)
        return;
    else
    {
        print(os, theRoot->getLeft());
        os << theRoot->getData() << " ";
        print(os, theRoot->getRight());
    }
}

//insert: public method
void BinaryTree::insert(int value)
{
    if(root == NULL)
        root = new node(value);
    else
        insert(root,value); //call private insert
}

//insert: private method
void BinaryTree::insert(node* root, int val)
{
    if(val < root->getData())
    {
        //Traverse the left subtree
        if(root->getLeft() == NULL)
        {
            //insert new node here.
            root->setLeft(new node(val));
        }
        else
        {
            //recursive call to traverse left subtree
            insert(root->getLeft(),val);
        }
    }
    else
    {
        //Traverse the right subtree
        if(root->getRight() == NULL)
        {
            //insert new node here
            root->setRight(new node(val));
        }
        else
        {
            //recursive call to traverse right subtree
            insert(root->getRight(),val);
        }
    }
}//end insert

//clear: Public method
void BinaryTree::clear()
{
    if(root == NULL)
        return;
    else
    {
        clear(root); //call private clear()
        root = 0; //tree is empty
    }
}//end clear

//clear: private, recursive method
void BinaryTree::clear(node* theRoot)
{
    if(theRoot == NULL)
        return;
    else
    {
        clear(theRoot->getLeft());
        clear(theRoot->getRight());
        delete theRoot;
    }
}//end clear
```

/*--------------------------------------------------------------*/

The following program tests the BinaryTree class.

/*--------------------------------------------------------------*/

/* filename: testBTree
   ... */

#include<iostream> //Required for cout.
#include "BinaryTree.h" //Required for BinaryTree.
using namespace std;

int main()
{
    BinaryTree bt; //Test default constructor
    bt.insert(2); //Test insert on empty tree.
    bt.insert(10); //Test insert to right subtree.
    bt.insert(-2); //Test insert to left subtree.
    bt.print(cout); //Test print method.
    bt.clear(); //Test clear method.
    bt.print(cout);
    return 0;
}

The output from a sample run of our test program is shown below:

```
-2 2 10
tree is empty
```

Now that a working version of a BinaryTree has been written and tested, we will write a class template to represent a generic binary tree, and test it against the working version.

## 10.5 Class Templates

The declaration of a class template must begin with an expression of the form:
`template < typename identifier >`
as illustrated in the following declaration of a class template to represent a node on a binary tree:

```
```cpp
/* .................... class declaration for node template .................... */
/* .................... filename: nodeTemplate.h .................... */

#ifndef TNODE_H
#define TNODE_H

template < typename T >
class Node
{
   // Private attributes
   private:
      T data;
      Node *left;
      Node *right;

   // Public interface.
   public:
      Node(); // Default constructor
      Node(T); // Parameterized constructor

      // Accessors
      Node * getLeft() const;
      Node * getRight() const;
      T getData() const;

      // Mutators
      void setLeft(Node *);
      void setRight(Node *);
      void setData(T v);
};

#endif
/* .................... */
```
```

Notice that the identifier T replaces int in the class template declaration. The implementation of this class template follows.

```
```cpp
/* .................... Class implementation for Node template .................... */
/* .................... filename: nodeTemplate.cpp .................... */

#include "nodeTemplate.h" // Required for Node.
using namespace std;
```
```
