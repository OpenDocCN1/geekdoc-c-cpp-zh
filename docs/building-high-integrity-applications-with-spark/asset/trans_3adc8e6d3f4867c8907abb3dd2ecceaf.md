
最重要的情形之一是：包规范在 SPARK 中，而相应的包体不在 SPARK 中。这允许你从 SPARK 代码调用非 SPARK 包中的子程序。作为一个例子，考虑以下变量包 `Interval_Tree` 的简化规范，该包封装了一个以结构化方式存储实数区间的对象。该包更贴近实际的版本还会包含额外的区间树操作。

```ada
package Interval_Tree
  with
    SPARK_Mode   => On,
    Abstract_State => Internal_Tree,
    Initializes    => Internal_Tree
is
  type Interval is
    record
      Low : Float;
      High : Float;
    end record;

  -- Inserts Item into the tree.
  procedure Insert (Item : in Interval)
    with
      Global  => (In_Out => Internal_Tree),
      Depends => (Internal_Tree => (Internal_Tree, Item)),
      Post    => Size = Size'Old + 1;

  function Size return Natural
    with
      Global => (Input => Internal_Tree);

  -- Destroys the tree. After this call, the tree can be reused.
  procedure Destroy
    with
      Global => (In_Out => Internal_Tree),
      Post   => Size = 0;

end Interval_Tree;
```

区间树可用于高效判断给定区间是否与一组已有区间中的任意一个重叠，以及执行类似操作。这里为便于说明，区间仅表示为一个保存两个浮点值的记录。该规范带有设置为 `On` 的 `SPARK_Mode` 方面，以表明它打算位于 SPARK 中。使用 `On` 是可选的；只要提到了 `SPARK_Mode`，就假定其取值为 `On`，除非另有说明。也可以改用 `SPARK_Mode` pragma。这两种形式含义相同。使用哪一种只是风格问题。

包规范中的子程序声明带有常见的 SPARK 方面，如 `Global`、`Depends` 和 `Post`。尽管本示例没有展示，但也可以提供前置条件。在对调用该包中子程序的代码进行分析时，SPARK 工具会以通常方式使用这些方面。

下面是包 `Interval_Tree` 的完整包体。该包体只展示了示例规范中所声明子程序的实现，以及必要的支持类型声明。

```ada
with Ada.Unchecked_Deallocation;
package body Interval_Tree
    with
        SPARK_Mode => Off
is
    type Tree_Node;
    type Tree_Node_Access is access Tree_Node;
    type Tree_Node is
        record
            Data      : Interval;
            Maximum   : Float;
            Parent    : Tree_Node_Access := null;
            Left_Child : Tree_Node_Access := null;
            Right_Child : Tree_Node_Access := null;
        end record;

    -- Instantiate a procedure for deallocating node memory
    procedure Deallocate_Node is new Ada.Unchecked_Deallocation
        (Object => Tree_Node,
         Name   => Tree_Node_Access);

    type Tree is
        record
            Root : Tree_Node_Access := null;
            Count : Natural := 0;
        end record;

    T : Tree;  -- The actual tree in this variable package

    procedure Insert (Item : in Interval) is
        New_Node : Tree_Node_Access; -- local to Insert, global to Subtree_Insert

        procedure Subtree_Insert (Pointer : in not null Tree_Node_Access) is
        begin
            if Item.Low <= Pointer.Data.Low then
                if Pointer.Left_Child = null then
                    Pointer.Left_Child := New_Node;
                    New_Node.Parent := Pointer;
                else
                    Subtree_Insert (Pointer.Left_Child);
                    Pointer.Maximum :=
                        Float'Max (Pointer.Maximum, Pointer.Left_Child.Maximum);
                end if;
            else
                if Pointer.Right_Child = null then
                    Pointer.Right_Child := New_Node;
                    New_Node.Parent := Pointer;
                else
                    Subtree_Insert (Pointer.Right_Child);
                    Pointer.Maximum :=
                        Float'Max (Pointer.Maximum, Pointer.Right_Child.Maximum);
                end if;
            end if;
        end Subtree_Insert;

    begin
        New_Node := new Tree_Node'(Data => Item,
                                    Maximum => Item.High,
                                    others => <>);
        if T.Root = null then
            T.Root := New_Node;
        else
            Subtree_Insert (T.Root);
        end if;
        T.Count := T.Count + 1;
    end Insert;

    function Size return Natural is
    begin
        return T.Count;
    end Size;

    procedure Destroy is

        procedure Deallocate_Subtree (Pointer : in out Tree_Node_Access) is
        begin
            if Pointer /= null then
                Deallocate_Subtree (Pointer.Left_Child);
                Deallocate_Subtree (Pointer.Right_Child);
                Deallocate_Node (Pointer);
            end if;
        end Deallocate_Subtree;

    begin
        Deallocate_Subtree (T.Root);
        T.Count := 0;
    end Destroy;

end Interval_Tree;
```

这个变量包体中的树数据结构使用指针²（访问类型）和动态分配的内存，以便树在程序执行期间可以按需增长到任意大小。由于这些构造在 SPARK 中不合法，因此通过将 `SPARK_Mode` 方面设置为 `Off`，显式声明该包体不在 SPARK 中。在这种情况下，必须显式设置包体的 SPARK 模式。因为包的规范已显式标记为在 SPARK 中，所以除非另有说明，工具会假定包体也在 SPARK 中。

由于包体不在 SPARK 中，因此不必精化规范中声明的抽象状态。此外，SPARK 工具不会验证包体中的子程序是否符合其声明的数据和流依赖契约，也不会尝试证明代码不存在运行时错误，以及子程序始终遵守其声明的后置条件。确保代码正确性的责任落在程序员身上，并需要配合适当的测试。

然而，重要的是要注意，前置条件和后置条件是 Ada 的一部分，因此 Ada 编译器会像往常一样加入运行时检查，以验证后置条件（在本例中），具体取决于编译包规范时生效的断言策略。如果后置条件失败，将引发 `Assertion_Error` 异常³，然后该异常会传播到 SPARK 代码中。对于任何未处理的 `Constraint_Error` 或 `Storage_Error` 异常，或者就此而言，包体中可能引发的任何其他未处理异常，情况也是如此。

这似乎有问题，因为 SPARK 代码不能定义任何异常处理程序来处理其调用的非 SPARK 代码中的异常。人们可能希望所有这类情况都能在测试期间被捕获，但即使不能，也仍然可以从一个不在 SPARK 中的高层“main”子程序调用 SPARK 代码，并在其中包含异常处理程序，以处理底层非 SPARK 子程序引发的任何意外异常。

包体中的子程序也可以捕获它们可能产生的所有异常（除了前置条件和后置条件失败所引发的 `Assertion_Error` 异常），并将其转换为错误状态码。然而，如果该包还要被非 SPARK 代码调用，而在这些代码中异常处理既自然又方便，那么这种方法可能并不理想。正如我们在第 7.1.2 节中所示，可以通过创建一个特殊的包装包来管理这种情况。

前一个示例展示了一个变量包，但如果你想以类型包的形式提供区间树呢？这将允许用户创建多个独立的树对象。像通常一样，可以通过声明一个私有类型来表示树本身，并在包规范中提供一个私有部分，向编译器详细说明树类型的性质。然而，该私有部分需要使用非 SPARK 构造，在本例中就是访问类型。幸运的是，可以只将规范的私有部分标记为不在 SPARK 中，如下所示：

```ada
private with Ada.Finalization;
package Interval_Trees
  with SPARK_Mode => On
is
  type Interval is
    record
      Low : Float;
      High : Float;
    end record;

  type Tree is limited private;

  -- Inserts Item into tree T.
  procedure Insert (T : in out Tree; Item : in Interval)
    with Global => null,
         Depends => (T => (T, Item));

  function Size (T : in Tree) return Natural
    with Global => null;

private
  pragma SPARK_Mode (Off);
```
