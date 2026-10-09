
```cpp
void visitPlus(NodePlus& node) override
    debug(node, "PLUS");
void visitMinus(NodeMinus& node) override
    debug(node, "MINUS");
void visitAdd(NodeAdd& node) override
    debug(node, "ADD");
// ...
void visitSpot(NodeSpot& node) override debug(node, "SPOT");
void visitIf(NodeIf& node) override
    {
        debug(node, string("IF(").to_string(node.firstElse)+"));
    }
void visitConst(NodeConst& node) override
    {
        debug(node, string("CONST").to_string(node.val)+"));
    }
void visitVar(NodeVar& node) override
    {
        debug(node, string("VAR[")+node.name+"]")+to_string(node.index));
    }
```

除了 `if`、`const` 和 `var` 节点外，所有节点都会调用 `debug()` 方法并传递一个识别节点类型的字符串。我们稍后会回到这个 `debug()` 方法。`if`、`const` 和 `var` 节点也会调用 `debug()`，但在传递类型外，还会传递它们的内部数据，以便我们也能看到这些。

让我们来看看双重分发是如何工作的。当调试器访问某个节点时（例如一个加法节点），它会调用节点上的虚拟 `acceptVisitor()` 方法，并将自身的引用作为参数传递。该调用通过经典的函数重载解析到 `NodeAdd` 重写的 `acceptVisitor()`：

```cpp
void NodeAdd::acceptVisitor(Visitor& visitor)
{
    visitor.visitAdd(*this);
}
```

# 4. 现代计算金融

这反过来会调用我们具体访问者（在本例中为 `Debugger`）的重写的 `visitAdd()` 方法，再次通过经典的类重写实现，因为作为参数传递给 `acceptVisitor()` 的 `Visitor` 类引用携带了它的具体类型。

## 访问者 (Visitors)

在模拟过程中执行语句 `x = y` 时，评估器必须查找一个名为 `y` 的变量并读取其值，然后查找另一个名为 `x` 的变量的地址，并将 `y` 的值写入其中。在所有模拟场景中，每条包含变量的语句都会发生这些查找，这导致了不可接受的性能损耗。我们对脚本化产品的评估性能需要与高效的硬编码定价器相匹配。如果我们在运行时反复查找名称，这是无法实现的。我们需要评估器能够直接获取内存中变量的值和地址。因此，变量必须经过预索引处理，这样一来，如果 `x` 的索引为 3 且 `y` 的索引为 7，`x = y` 将被评估器读取为 `var[3] = var[7]` 并进行直接随机访问。

为了在模拟之前进行索引，我们使用了一个名为变量索引器（variable indexer）的访问者。这个特定的访问者像所有访问者一样遍历所有树，但在访问变量时，它会对它们进行计数并在节点上设置唯一的索引。索引不仅是一个强迫性的性能需求，它还突显了访问者的一些理想特性，这些特性在调试器中并不明显：

- 1. 访问者只重写它们感兴趣的节点的方法，在本例中，即变量节点。得益于基础访问者类中的默认访问方法，整个树仍然会被遍历。在这里，某些访问者的代码可能非常紧凑。
- 2. 访问者持有状态，并在访问树的序列以及遍历语句和事件时携带该状态，根据所访问的节点更新其状态计数，并在访问当前节点时使用在后继节点上收集的信息。在本例中，我们的索引器维护了一个所有遇到过的变量的映射。
- 3. 访问者不仅限于读取表达式树中存储的信息。变量索引器会将变量的索引写入变量节点。其他访问者甚至可以修改树的结构。

首先，我们需要为变量节点添加索引：

```cpp
struct NodeVar : Node
{
    string name;
    unsigned index;

    void acceptVisitor(Visitor& visitor) override;
};
```

然后，我们开发该访问者。这个特定的访问者只针对变量停止，因此它重写了每个 `visitVar()` 方法，使其代码非常紧凑。此外，它携带了一个自其构造以来访问的所有变量的状态，表现为从变量名到其索引的映射。

# 52 现代计算金融

```cpp
#include <map>

class VarIndexer : public Visitor {
    // 状态
    map<string, unsigned> myVarMap;

public:
    // 变量索引器：构建名称到索引的映射
    // 并将索引写入变量节点
    void visit(VarNode& node) override {
        auto varit = myVarMap.find(node.name);
        if(varit == myVarMap.end())
            node.index = myVarMap[node.name].size();
        else
            node.index = varit->second;
    }
};
```

就是这样。当它访问一个变量时，它会在映射中查找该名称。如果找到，它会在节点上设置相应的索引。如果没找到，它会将该名称添加到映射中以备日后参考，并使用下一个索引（即当前映射的大小）在节点上设置相同的索引。整个代码仅占了三行，这足以访问者索引跨越语句和事件的树集合中的所有变量。我们需要添加一个方法来生成生成的变量名数组：

```cpp
class VarIndexer : public Visitor {
    // 状态
    map<string, unsigned> myVarMap;

public:
    // 访问变量名向量
    // 访问所有事件的 v[index]-name
    vector<string> v(myVarMap.size()) const {
        for (auto varMapit = myVarMap.begin();
             varMapit != myVarMap.end(); ++varMapit) {
            v[varMapit->second] = varMapit;
        }
    }
};
```

# 56 现代计算金融

```cpp
virtual void visitArguments( const Node& node)
{
    for(auto& arg : node.arguments) arg->acceptVisitor(*this);
}
```

public:

// 访问（子）树的入口点

void visit(const ExprTree& tree)

{

    tree->acceptVisitor(*this);

}

// 所有具体节点的默认访问器，

// 除非被重写，否则会访问参数

virtual void visitUPlus(const NodeUplus& node)

{

    visitArguments(node);

}

virtual void visitMinus(const NodeUminus& node)

{

    visitArguments(node);

}

virtual void visitAdd(const NodeAdd& node)

{

    visitArguments(node);

}

//

virtual void visitVar(const NodeVar& node)

{

    visitArguments(node);

}
```

并且我们在节点类中支持常量访问器（constVisitors）：

```cpp
struct Node
{
