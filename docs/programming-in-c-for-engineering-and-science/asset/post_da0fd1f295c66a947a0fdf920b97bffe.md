
For the next step, one of the two sublists, the left half or the right half, must be searched and both must therefore be accessible from this node. This is possible if we maintain two links, one to each of these sublists. Because these sublists are searched in the same manner, these links should refer to nodes containing the middle elements in these sublists:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_672_0.png)

By the same reasoning, in the next step, links from each of these “second-level” nodes are needed to access the middle elements in their sublists:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_672_1.png)

The resulting structure is easier to visualize if we “stretch it out” into two dimensions so that it has a treelike shape:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_672_2.png)

This structure is called a binary search tree and is a special kind of binary tree, which is a special instance of a more general structure called a tree.

## 16.4.1 Tree Terminology and Examples

A tree consists of a finite collection of nodes linked together in such a way that if the tree is not empty, then one of the nodes, called the root, has no incoming links, but every other node in the tree can be reached from the root by following a unique sequence of consecutive links.

Trees derive their names from the treelike diagrams that are used to picture them. For example, the diagram on the next page shows a tree having nine vertices in which the node labeled 1 is the root. As this diagram indicates, trees are usually drawn upside down, with the root at the top and the leaves—nodes with no outgoing links—at the bottom. Nodes that are directly accessible from a given node (by using only one link) are called the children of that node, and a node is said to be the parent of its children. For example, in the following tree, node 3 is the parent of nodes 5, 6, and 7, and these nodes are the children of node 3 and are called siblings.

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_673_0.png)

Applications of trees are many and varied. For example, a genealogical tree such as the following is a convenient way to picture a person's descendants:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_673_1.png)

Game trees are used to analyze games and puzzles. Parse trees are used to check a program's syntax. For example, the following is a parse tree for the expression 2 * (3 + 4):

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_673_2.png)

## 16.4.2 Examples of Binary Trees

**Binary trees** are trees in which each node has at most two children. They are especially useful in modeling processes in which some experiment or test with two possible outcomes (for example, off or on, 0 or 1, false or true, down or up, yes or no) is performed repeatedly. For example, the following binary tree might be used to represent the possible outcomes of flipping a coin three times:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_674_0.png)

Each path from the root to one of the leaf nodes corresponds to a particular outcome, such as HTH (a head followed by a tail followed by another head), as highlighted in the diagram.

Similarly, a binary tree can be used in coding problems such as encoding and decoding messages transmitted in Morse code, a scheme in which characters are represented as sequences of dots and dashes, as shown in the following table:

|   |   |   |   |   |
|---|---|---|---|---|
| A | • — | J | •• — — | S | ••• | 2 | •• — — — |
| B | — ••• | K | — • — | T | — | 3 | ••• — — |
| C | — • — • | L | •• — • | U | •• — | 4 | •••• — |
| D | — •• | M | — — | V | ••• — | 5 | ••••• |
| E | • | N | — • | W | • — — | 6 | — •••• |
| F | •• — • | O | — — — | X | — •• — | 7 | — — ••• |
| G | — — • | P | • — — • | Y | — • — — | 8 | — — — •• |
| H | •••• | Q | — — • — | Z | — — •• | 9 | — — — — • |
| I | •• | R | • — • | 1 | • — — — — | 0 | — — — — — |

In this case, the nodes represent the characters and each link from a node to its children is labeled with a dot or a dash, according to whether it leads to a left child or to a right child, respectively. Thus, part of the tree for Morse code is

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_674_1.png)

The sequence of dots and dashes labeling a path from the root to a particular node corresponds to the Morse code for that character; for example, •• is the code for I, and — • is the code for N.

Decision-making processes can be modeled as a series of “yes-or-no” questions, and a binary tree can thus be used to model that process. Each nonleaf node is used to store a question, and if an affirmative answer to a question leads to another question, then the two nodes are connected with a link labeled “yes.” Similarly, if a negative answer to a question leads to another question, then the two nodes are connected with a link labeled “no.” Because there are only two choices for each question, the resulting structure is a binary tree with decisions at its leaf nodes. The problem of choosing a single choice from among many choices is solved simply by descending through the tree until a leaf node (i.e., a decision) is reached.

For problems in some areas, solutions can be obtained by designing decision trees that mimic the choices experts would make in solving these problems. For example, programs to control a robot that welds automobile components on an assembly line are based on the knowledge of an expert welder. Programs to help a person prepare their income tax returns have some of the expertise of a tax accountant encoded within them. Similarly, programs that lead a person through the steps of writing a will have some of the expertise of an estate lawyer encoded within them. In general, programs that exhibit expertise in some area through the use of a knowledge base are called expert systems, and the study of such systems is one of the branches of artificial intelligence. A simple example of an expert system is given on the text’s website.

## 16.4.3 Implementing Binary Trees

A binary tree can be represented by a multiply linked structure in which each node has two links, one connecting it to its left child and the other connecting it to its right child, or which are null if the node does not have a left or right child:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_675_0.png)

A leaf node is thus characterized by myLeft and myRight both being null:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_675_1.png)

If we represent such nodes by a class named Node that has three public data members,

```
template <typename DataType>
class Node
```

> ⁶ A struct in C, and thus also provided in C++, is a class whose data and function members are public.

```
{
public:
    //... Node function members go here
    DataType myValue;
    Node *  myLeft;
    Node *  myRight;
};
```

we can then use it in a BinaryTree class template:

```
template <typename DataType>
class BinaryTree
{
public:
    // ... Binary tree function members go here

private:
    // ... Declaration of class Node goes here
    Node * myRoot;
    int    mySize;
};
```

The data member myRoot is a pointer to the node that is the root of the tree, and mySize is used for convenience to keep track of the number of nodes in the tree. Given such a class, the binary tree

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_676_0.png)

can be represented as the following linked structure:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_676_1.png)

## 16.4.4 Binary Search Trees

In the preceding binary tree, the value in each node is greater than all values in its left subtree (if there are any) and less than all values in its right subtree (if there are any). A binary tree having this property is called a binary search tree (BST) because, as noted at the beginning of this section, it can be searched using an algorithm much like the binary search algorithm for lists:

### Search Algorithm for a BST

- 1. Initialize a pointer ptr to the node containing the root and found to false.
- 2. While ptr is not null and found is false, do the following:
  - If the item being sought is:
    - Less than the value in the node pointed to by ptr
    - Set ptr equal to its left link;
    - Greater than the value in the node pointed to by ptr
    - Set ptr equal to its right link;
    - Else
    - Set found to true.

To illustrate, suppose we wish to search the preceding BST for 25. We begin at the root, and because 25 is less than the value 46 in this root, we know that the desired value is located to the left of the root; that is, it must be in the left subtree, whose root is 17:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_677_0.png)

Now we continue the search by comparing 25 with the value in the root of this subtree. Because 25 > 17, we know that the right subtree should be searched:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_677_1.png)

Examining the value in the root of this one-node subtree locates the value 25.

Similarly, to search for the value 55, after comparing 55 with the value in the root, we are led to search its right subtree:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_677_2.png)
