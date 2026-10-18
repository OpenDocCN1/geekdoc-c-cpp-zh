
我们输入到 ComputeValueFrom 函数的是一个节点向量，由第 [1] 行的 NodeVec 定义。这对应于图 6.19 中的输入 RPN 表达式 `5 3 4 + *`，但其中的元素是来自 TNode 层次结构（第 6.6.4 节）的节点对象。返回值将由 LeafValType 表示，其别名在第 [4] 行定义。

如果输入 `node_vec` 中有任何节点，则会在第 [21] 行创建保存 LeafValType 对象的辅助栈 `auxStack`。然后，从第 [25] 行开始的 range 循环中，`node_vec` 中的节点会从左到右进行处理，如图 6.19 所示。但问题如下：尽管 `node_vec` 的所有元素都是指向 TNode 基类的智能指针，但实际指针指向的是 TNode 层次结构中的不同对象。例如，对于我们的简单表达式，我们将有三个 LeafValType，后面跟着一个 PlusOperator 和一个 MultOperator。我们需要像之前 RPN 处理算法中所描述的那样对它们进行不同处理，但我们只有 TNode 指针。因此，我们必须弄清楚如何在运行时区分一个指向 LeafValType 的 TNode 指针和另一个指向 PlusOperator 的 TNode 指针。在 C++ 中，RTTI 机制派上了用场，正如我们在第 3.19.1 节讨论 C++ 运算符 GROUP 2 时所提到的。这两种 RTTI 结构是 `typeid` 和 `dynamic_cast` 运算符。`typeid` 允许我们检查通过指针或引用所指对象的类型，即使该指针或引用指向的是基类，而相关对象的类派生自该基类。另一方面，在运行时，`dynamic_cast` 会尝试将指针或引用执行受检查的转换，转换为所请求的类型。如果转换的类型沿继承层次结构向上、向下或侧向移动，则转换将成功。否则，如果尝试 `dynamic_cast<a_pointer>`，将返回 `nullptr`。如果是 `dynamic_cast<a_reference>`，则会抛出 `std::bad_cast` 异常。我们将在代码中使用这些特性。首先，为了区分 LeafValType 对象，第 [29] 行使用 NumberLeafNode 的 `typeid` 来验证 node 所持有的对象的 `typeid`。如果它们一致，则将该对象的值压入 `auxStack`。具体来说，在第 [32] 行，node 被转换为指向 NumberLeafNode 对象的指针，从中读取值并压入栈中。但这是如何实现的呢？由于 node 是 `std::unique_ptr`，它与 NumberLeafNode 类不兼容。然而，它内置了一个重载的转换运算符，可转换为所持有类的指针。因此，`std::unique_ptr` 可以用于所有需要指向所持有对象的指针或引用的代码中。因此，可以通过将 node 转换为 NumberLeafNode 对象来调用 GetValue。

```
using NodeVec = ExpressionTreeBuilderInterpreter::NodeStack::DataContainer;

using LeafValType = double;

// Computes value of the stack
LeafValType ComputeValueFrom( const NodeVec & node_vec )
{
    auto retVal { 0.0 };

    const auto kNumOfElements = node_vec.size();
    if ( kNumOfElements == 0 )
    {
        return retVal;
    }
```

# 清单 6.29 直接从存储在栈中的 RPN 表示计算表达式值的函数（位于 *Parser, NodeStackConverters.cpp* 中）。

[PAGE 493]

# 清单 6.29（续）

```
void RPN_Value_Test( void )
{
#if BUILD_THE_TREE == 1
    assert( false );        // A fuse to ensure we compiled with the proper parameter
#endif
}
```

6 在 STL 中没有预定义的 div_by_zero 异常，因此我们可以使用 `std::overflow_error` 或 `std::underflow_error`，或者创建一个自定义异常类。
