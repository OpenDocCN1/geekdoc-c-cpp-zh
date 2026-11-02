
```
type Tree_Node;
type Tree_Node_Access is access Tree_Node;
type Tree_Node is
  record
    Data : Interval;
    Maximum : Float;
    Parent : Tree_Node_Access := null;
    Left_Child : Tree_Node_Access := null;
    Right_Child : Tree_Node_Access := null;
  end record;

type Tree is new Ada.Finalization.Limited_Controlled with
  record
    Root : Tree_Node_Access := null;
    Count : Natural := 0;
  end record;

overriding procedure Finalize (T : in out Tree);

end Interval_Tree;
```

在这种情况下，必须使用 SPARK_Mode 的 pragma 形式，因为 Ada 不允许将方面仅应用于包规范的私有部分。pragma SPARK_Mode (Off) 必须出现在私有部分的顶部，将整个私有部分标记为不在 SPARK 中。

此示例还利用了 Ada 自动终结对象的机制⁴，因此在这种情况下程序员无需调用 “destroy” 过程。为此，必须使用 Ada.Finalization。然而，由于该包仅用于支持私有部分，因此可以使用我们在 3.5.2 节中介绍的 with 子句的特殊形式来引入它。private with 使该包的资源仅在私有部分可用。

也可以将各个子程序标记为处于 SPARK 中。这在包规范需要使用非 SPARK 构造，但包中的某些子程序仍可给出 SPARK 声明的情况下很有用。随后，SPARK 代码可以调用带有 SPARK 声明的子程序，即使它可能无法使用外层包的所有功能。

类似地，包体中的子程序体可以视情况标记为在 SPARK 内或 SPARK 外。这使你可以在合适的代码上使用 SPARK 工具，而无需为了同一包中的其他子程序人为避免完整的 Ada 特性，从而造成不自然的设计。

关于 SPARK 模式有一条重要的一致性规则：一旦 SPARK 模式被关闭，就不能再为任何从属构造重新打开它。为说明这一点，包被认为包含四个部分：

- 1. 规范的可见部分
- 2. 规范的私有部分
- 3. 包体
- 4. 包体中出现在 **begin** 之后的精化代码

该一致性规则意味着，如果对其中某个部分显式关闭了 SPARK 模式，那么就不能在后面的部分中重新打开它。例如，如果包的包体关闭了 SPARK 模式，那么就不能再在该包的精化代码中重新打开 SPARK 模式。

此外，如果对某个部分打开了 SPARK 模式，则假定它对所有后续部分都打开，除非显式关闭。因此，在包的规范中将 SPARK_Mode 设置为 On 会声明该包的所有部分都处于 SPARK 中，除非对后面的部分将 SPARK_Mode 显式设置为 Off。

### 7.1.2 包装器包

如前所述，只要该库包的规范（或至少被调用子程序的规范）处于 SPARK 中，就允许 SPARK 调用具有非 SPARK 包体的库包中的代码。即使被调用子程序的声明没有明确标记为处于 SPARK 中，也可能仍然允许 SPARK 代码使用 7.1.3 节所述的自动 SPARK 模式来调用它们。

然而，非 SPARK 库包中的错误很可能通过异常来报告，因为这是完整 Ada 中正常的错误处理方式。因此，需要某种手段将异常转换为 SPARK 风格错误处理所需的状态码。此外，如果非 SPARK 库包具有非 SPARK 规范，仍可能通过适当的翻译和转换使其可从 SPARK 调用。完成这些工作需要构造一个包装器包，该包提供 SPARK 规范，并包含仅将其调用转发到底层库包的子程序。

作为示例，考虑 7.1.1 节中描述的 Interval_Tree 包。该包恰好具有 SPARK 规范，但包体中出现的异常仍可能传播到 SPARK 代码中。为处理此问题，我们创建一个新包 Interval_Tree_Wrapper，其规范与 Interval_Tree 的规范非常相似，如下所示：

```
with Interval_Tree;
package Interval_Tree_Wrapper
    with
        SPARK_Mode => On,
        Abstract_State => Underlying_Tree,
        Initializes => Underlying_Tree
is

    type Interval is new Interval_Tree.Interval;

    type Status_Type is (Success, Insufficient_Space, Logical_Error);

    -- Inserts Item into the tree.
    procedure Insert (Item : in Interval;
                      Status : out Status_Type)
        with
            Global => (In_Out => Underlying_Tree),
            Depends => (Underlying_Tree => (Underlying_Tree, Item),
                        Status => Underlying_Tree),
            Post => (Size'Old = (if Status = Success then Size - 1 else Size)));

    function Size return Natural
        with
            Global => (Input => Underlying_Tree);

    -- Destroys the tree. After this call the tree can be reused.
    procedure Destroy
        with
            Global => (In_Out => Underlying_Tree),
            Post => Size = 0;

end Interval_Tree_Wrapper;
```

该规范与 Interval_Tree 的规范之间的主要区别在于：引入了一个状态类型，并且可能失败的子程序——此处为 Insert——被修改为返回状态指示。

包装器包还为底层包提供的类型（此处为类型 Interval）引入了自己的类型。这使包装器包能够自包含，而无需其客户端 with 底层包。

还要注意，Insert 的 SPARK 方面与底层过程版本略有不同。流依赖契约增加了 Status 对 Underlying_Tree 的依赖。此外，后置条件被改为断言：当且仅当子程序成功返回时，树的大小才会增加。

将后置条件写成如下形式会更自然：

```
Post => (if Status = Success
    then Size = Size'Old + 1
    else Size = Size'Old);
```

然而，Ada 不允许在可能不会被求值的上下文中（例如条件表达式的某个分支中）对函数调用的前缀使用 'Old 属性。回想一下，'Old 意味着在进入子程序时保存前缀表达式的值。当结果可能不需要时，调用函数是不可取的。此处，Size'Old 在条件表达式的两个分支中都被使用。尽管如此，Ada 的规则在此情况下禁止这样做。

Underlying_Tree 状态抽象旨在表示底层包的内部树。严格来说，Interval_Tree_Wrapper 没有内部状态，因此为它声明任何 Abstract_State 都是“谎言”。SPARK 工具不会注意到这个谎言，因为正如你将看到的，Interval_Tree_Wrapper 的包体不在 SPARK 中，因此不会被工具检查。然而，如果对底层包的唯一访问是通过包装器，那么这个谎言并不是真正的问题，因为包装器包实际上承担了被包装包的内部状态，就像可以说包装纸包含与它所包装的盒子相同的礼物一样。

然而，在此情况下，Interval_Tree 具有 SPARK 规范，并且可能被愿意将异常传递到更高层的 SPARK 代码直接调用。为了让 SPARK 工具正确理解其他代码与包装器包之间的关系，有必要如实说明包装器包在做什么。可以通过不在 Interval_Tree_Wrapper 上定义 Abstract_State，而是在前面提到 Underlying_Tree 的 SPARK 方面中显式引用 Interval_Tree.Internal_Tree 来实现。

包装器包的包体包含相对简单的子程序，这些子程序包装底层库包的子程序。以下是包装器包中 Insert 的实现：

```
procedure Insert (Item : in Interval;
    Status : out Status_Type) is
begin
    Interval_Tree.Insert (Interval_Tree.Interval (Item));
```
