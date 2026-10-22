
![](img/7ea3c39173f146f675b63b146d1535f3_180_0.png)

**Figure 5.9** An expression tree for 4x(2x + a) − c.

An important decision in the design of a pointer-based node implementation is whether the same class definition will be used for leaves and internal nodes. Using the same class for both will simplify the implementation, but might be an inefficient use of space. Some applications require data values only for the leaves. Other applications require one type of value for the leaves and another for the internal nodes. Examples include the binary trie of Section 13.1, the PR quadtree of Section 13.3, the Huffman coding tree of Section 5.6, and the expression tree illustrated by Figure 5.9. By definition, only internal nodes have non-empty children. If we use the same node implementation for both internal and leaf nodes, then both must store the child pointers. But it seems wasteful to store child pointers in the leaf nodes. Thus, there are many reasons why it can save space to have separate implementations for internal and leaf nodes.

As an example of a tree that stores different information at the leaf and internal nodes, consider the expression tree illustrated by Figure 5.9. The expression tree represents an algebraic expression composed of binary operators such as addition, subtraction, multiplication, and division. Internal nodes store operators, while the leaves store operands. The tree of Figure 5.9 represents the expression 4x(2x + a) − c. The storage requirements for a leaf in an expression tree are quite different from those of an internal node. Internal nodes store one of a small set of operators, so internal nodes could store a small code identifying the operator such as a single byte for the operator’s character symbol. In contrast, leaves store variable names or numbers, which is considerably larger in order to handle the wider range of possible values. At the same time, leaf nodes need not store child pointers.

C++ allows us to differentiate leaf from internal nodes through the use of class inheritance. A base class provides a general definition for an object, and a subclass modifies a base class to add more detail. A base class can be declared for binary tree nodes in general, with subclasses defined for the internal and leaf nodes. The base class of Figure 5.10 is named **VarBinNode**. It includes a virtual member function named **isLeaf**, which indicates the node type.

Subclasses for the internal and leaf node types each implement **isLeaf**. Internal nodes store child pointers of the base class type; they do not distinguish their children’s actual subclass. Whenever a node is examined, its version of **isLeaf** indicates the node’s subclass.

Figure 5.10 includes two subclasses derived from class **VarBinNode**, named **LeafNode** and **IntlNode**. Class **IntlNode** can access its children through pointers of type **VarBinNode**. Function **traverse** illustrates the use of these classes. When **traverse** calls method **isLeaf**, C++’s runtime environment determines which subclass this particular instance of **root** happens to be and calls that subclass’s version of **isLeaf**. Method **isLeaf** then provides the actual node type to its caller. The other member functions for the derived subclasses are accessed by type-casting the base class pointer as appropriate, as shown in function **traverse**.

There is another approach that we can take to represent separate leaf and internal nodes, also using a virtual base class and separate node classes for the two types. This is to implement nodes using the **composite design pattern**. This approach is noticeably different from the one of Figure 5.10 in that the node classes themselves implement the functionality of **traverse**. Figure 5.11 shows the implementation. Here, base class **VarBinNode** declares a member function **traverse** that each subclass must implement. Each subclass then implements its own appropriate behavior for its role in a traversal. The whole traversal process is called by invoking **traverse** on the root node, which in turn invokes **traverse** on its children.

When comparing the implementations of Figures 5.10 and 5.11, each has advantages and disadvantages. The first does not require that the node classes know about the **traverse** function. With this approach, it is easy to add new methods to the tree class that do other traversals or other operations on nodes of the tree. However, we see that **traverse** in Figure 5.10 does need to be familiar with each node subclass. Adding a new node subclass would therefore require modifications to the **traverse** function. In contrast, the approach of Figure 5.11 requires that any new operation on the tree that requires a traversal also be implemented in the node subclasses. On the other hand, the approach of Figure 5.11 avoids the need for the **traverse** function to know anything about the distinct abilities of the node subclasses. Those subclasses handle the responsibility of performing a traversal on themselves. A secondary benefit is that there is no need for **traverse** to explicitly enumerate all of the different node subclasses, directing appropriate action for each. With only two node classes this is a minor point. But if there were many such subclasses, this could become a bigger problem. A disadvantage is that the traversal operation must not be called on a **NULL** pointer, because there is no object to catch the call. This problem could be avoided by using a flyweight (see Section 1.3.1) to implement empty nodes.

Typically, the version of Figure 5.10 would be preferred in this example if **traverse** is a member function of the tree class, and if the node subclasses are

```cpp
// Node implementation with simple inheritance
class VarBinNode {  // Node abstract base class
public:
    virtual ~VarBinNode() {}
    virtual bool isLeaf() = 0;      // Subclasses must implement
};

class LeafNode : public VarBinNode { // Leaf node
private:
    Operand var;                    // Operand value

public:
    LeafNode(const Operand& val) { var = val; } // Constructor
    bool isLeaf() { return true; }      // Version for LeafNode
    Operand value() { return var; }     // Return node value
};

class IntlNode : public VarBinNode { // Internal node
private:
    VarBinNode* left;               // Left child
    VarBinNode* right;              // Right child
    Operator opx;                   // Operator value

public:
    IntlNode(const Operator& op, VarBinNode* l, VarBinNode* r)
        { opx = op; left = l; right = r; } // Constructor
    bool isLeaf() { return false; }     // Version for IntlNode
    VarBinNode* leftchild() { return left; }   // Left child
    VarBinNode* rightchild() { return right; } // Right child
    Operator value() { return opx; }           // Value
};

void traverse(VarBinNode *root) {    // Preorder traversal
    if (root == NULL) return;         // Nothing to visit
    if (root->isLeaf())               // Do leaf node
        cout << "Leaf: " << ((LeafNode *)root)->value() << endl;
    else {                            // Do internal node
        cout << "Internal: "
             << ((IntlNode *)root)->value() << endl;
        traverse(((IntlNode *)root)->leftchild());
        traverse(((IntlNode *)root)->rightchild());
    }
}
```

**Figure 5.10** An implementation for separate internal and leaf node representations using C++ class inheritance and virtual functions.

```cpp
// Node implementation with the composite design pattern
class VarBinNode {  // Node abstract base class
public:
    virtual ~VarBinNode() {}      // Generic destructor
    virtual bool isLeaf() = 0;
    virtual void traverse() = 0;
};

class LeafNode : public VarBinNode { // Leaf node
private:
    Operand var;                  // Operand value
public:
    LeafNode(const Operand& val) { var = val; } // Constructor
    bool isLeaf() { return true; }      // isLeaf for LeafNode
    Operand value() { return var; }     // Return node value
    void traverse() { cout << "Leaf: " << value() << endl; }
};

class IntlNode : public VarBinNode { // Internal node
private:
    VarBinNode* lc;               // Left child
    VarBinNode* rc;               // Right child
    Operator opx;                 // Operator value
public:
    IntlNode(const Operator& op, VarBinNode* l, VarBinNode* r)
        { opx = op; lc = l; rc = r; }    // Constructor
    bool isLeaf() { return false; }    // isLeaf for IntlNode
    VarBinNode* left() { return lc; }  // Left child
    VarBinNode* right() { return rc; } // Right child
    Operator value() { return opx; }   // Value
    void traverse() { // Traversal behavior for internal nodes
        cout << "Internal: " << value() << endl;
        if (left() != NULL) left()->traverse();
        if (right() != NULL) right()->traverse();
    }
};

// Do a preorder traversal
void traverse(VarBinNode *root) {
    if (root != NULL) root->traverse();
}
```

**Figure 5.11** A second implementation for separate internal and leaf node representations using C++ class inheritance and virtual functions using the composite design pattern. Here, the functionality of traverse is embedded into the node subclasses.
