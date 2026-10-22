

![](img/7ea3c39173f146f675b63b146d1535f3_180_0.png)

**图 5.9** 4x(2x + a) − c 的表达式树。

在基于指针的节点实现的设计中，一个重要的决策是是否对叶子节点和内部节点使用相同的类定义。使用同一类来处理两者会简化实现，但可能是一种低效的空间使用方式。某些应用仅需要叶子节点的数据值。其他应用需要叶子节点一种类型的值，内部节点另一种类型的值。示例包括第 13.1 节的二叉 trie、第 13.3 节的 PR 四叉树、第 5.6 节的 Huffman 编码树，以及图 5.9 所示的表达式树。根据定义，只有内部节点才具有非空的子节点。如果我们对内部节点和叶子节点使用相同的节点实现，那么两者都必须存储子指针。但在叶子节点中存储子指针似乎是浪费的。因此，有很多理由说明将内部节点和叶子节点分开实现可以节省空间。

作为在叶子节点和内部节点存储不同信息的树的示例，考虑图 5.9 所示的表达式树。表达式树表示由加法、减法、乘法和除法等二元运算符组成的代数表达式。内部节点存储运算符，而叶子存储操作数。图 5.9 的树表示表达式 4x(2x + a) − c。表达式树中叶子节点的存储需求与内部节点大不相同。内部节点存储一组很小的运算符之一，因此内部节点可以存储一个小的代码来标识运算符，例如运算符字符符号的一个字节。相比之下，叶子存储变量名或数字，为了处理更宽范围的可能值，其大小要大得多。与此同时，叶子节点无需存储子指针。

C++ 允许我们通过使用类继承来区分叶子节点和内部节点。基类为对象提供通用定义，子类修改基类以添加更多细节。可以为二叉树节点一般声明一个基类，并为内部节点和叶子节点定义子类。图 5.10 的基类名为 **VarBinNode**。它包含一个名为 **isLeaf** 的虚成员函数，用于指示节点类型。

内部节点类型和叶子节点类型的子类各自实现 **isLeaf**。内部节点存储基类类型的子指针；它们不会区分其子节点的实际子类。每当检查一个节点时，其版本的 **isLeaf** 指示节点的子类。

图 5.10 包含两个从类 **VarBinNode** 派生的子类，名为 **LeafNode** 和 **IntlNode**。类 **IntlNode** 可以通过类型为 **VarBinNode** 的指针访问其子节点。函数 **traverse** 说明了这些类的使用。当 **traverse** 调用方法 **isLeaf** 时，C++ 的运行时环境确定这个 **root** 实例实际属于哪个子类，并调用该子类的 **isLeaf** 版本。方法 **isLeaf** 然后向其调用者提供实际的节点类型。派生子类的其他成员函数通过适当的类型转换基类指针来访问，如函数 **traverse** 所示。

我们也可以采用另一种方法来表示独立的叶子节点和内部节点，同样使用虚基类和两种类型的独立节点类。这就是使用 **组合设计模式** 实现节点。这种方法与图 5.10 的方法明显不同之处在于，节点类本身实现了 **traverse** 的功能。图 5.11 显示了实现。在这里，基类 **VarBinNode** 声明了一个成员函数 **traverse**，每个子类必须实现它。每个子类然后为其在遍历中的角色实现自己的适当行为。整个遍历过程是通过在根节点上调用 **traverse** 来调用的，这反过来会在其子节点上调用 **traverse**。

比较图 5.10 和图 5.11 的实现，各有优缺点。第一种方法不需要节点类知道 **traverse** 函数。使用这种方法，很容易向树类添加新方法，以对树节点执行其他遍历或其他操作。然而，我们看到图 5.10 中的 **traverse** 确实需要熟悉每个节点子类。因此，添加新的节点子类将需要修改 **traverse** 函数。相比之下，图 5.11 的方法要求对树进行的任何需要遍历的新操作也必须在节点子类中实现。另一方面，图 5.11 的方法避免了 **traverse** 函数需要知道节点子类的不同能力。那些子类处理了在自身上执行遍历的责任。一个次要的好处是，**traverse** 无需显式枚举所有不同的节点子类，为每个节点指定适当的操作。只有两个节点类时这是一个次要问题。但如果有许多这样的子类，这可能成为更大的问题。一个缺点是遍历操作不能在 **NULL** 指针上调用，因为没有对象来捕获调用。可以通过使用享元 [见第 1.3.1 节] 来实现空节点来避免这个问题。

通常，如果 **traverse** 是树类的成员函数，并且节点子类是

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

**图 5.10** 使用 C++ 类继承和虚函数实现独立的内部节点和叶子节点表示的实现。

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

**图 5.11** 使用 C++ 类继承和虚函数使用组合设计模式的独立内部节点和叶子节点表示的第二种实现。在这里，traverse 的功能嵌入到节点子类中。

