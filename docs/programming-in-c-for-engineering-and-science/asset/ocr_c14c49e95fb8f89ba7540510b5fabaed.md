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

![](bbox=[0.28, 0.62, 0.75, 0.72])

can be represented as the following linked structure:

![](bbox=[0.18, 0.8, 0.78, 0.95])