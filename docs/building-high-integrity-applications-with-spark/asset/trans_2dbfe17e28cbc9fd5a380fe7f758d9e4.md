

更困难的情况。然而，归根结底，为代码生成“证明”的是人，而不是工具，即便这些证明只是在头脑中完成的。工具只是用来检查人的工作。

作为最后一个示例，请考虑我们在第 167 页给出的 `Binary_Search` 过程的如下实现：

```ada
package body Searchers2
  with SPARK_Mode => On
is

  procedure Binary_Search (Search_Item : in  Integer;
                           Items       : in  Array_Type;
                           Found       : out Boolean;
                           Result      : out Index_Type) is

    Low_Index  : Index_Type := Items'First;
    Mid_Index  : Index_Type;
    High_Index : Index_Type := Items'Last;
begin
  Found := False;
  Result := Items'First;  -- Initialize Result to "not found" case.

  -- If the item is out of range, it is not found.
  if Search_Item < Items(Low_Index) or Items(High_Index) < Search_Item then
    return;
  end if;

  loop
    Mid_Index := (Low_Index + High_Index) / 2;
    if Search_Item = Items(Mid_Index) then
      Found := True;
      Result := Mid_Index;
      return;
    end if;

    exit when Low_Index = High_Index;

    pragma Loop_Invariant
      (Search_Item in Items(Low_Index) .. Items(High_Index));

    if Items(Mid_Index) < Search_Item then
      Low_Index := Mid_Index;
else
    High_Index := Mid_Index;
end if;

end loop;
end Binary_Search;

end Searchers2;
```

该实现是非递归的，也相对直接。要完成证明，必须给出合适的循环不变量。和往常一样，找到正确的循环不变量是整个问题中最棘手的部分。在给出不变量的位置，搜索项尚未被找到；如果它确实存在于数组中，那么它位于 `Low_Index` 到 `High_Index`（含两端）之间。借助所示的不变量，前面给出的 `Binary_Search` 实现即可得到证明：它永远不会出现运行时错误，并满足其强后置条件。

不幸的是，前面的实现存在一个严重缺陷。在某些情况下，循环会无限运行而没有任何进展。考虑 `Low_Index` 和 `High_Index` 相邻，且所考察的数组元素是自然数 10 和 20 的情况。假设搜索项是 20。此时实现计算出的 `Mid_Index` 等于 `Low_Index`。由于数组中该位置的元素（10）小于搜索项（20），实现将 `Low_Index` 设为 `Mid_Index` 的值，而这一操作不会改变任何东西。于是过程永久循环。

尽管工具已经证明该过程满足其后置条件，但这个结论只在过程最终会返回时才适用。我们尚未证明该过程在每种情况下都会终止。在第 6.5 节中，我们会讨论如何做到这一点。

## 6.5 循环变体

在上一节中我们看到，SPARK 工具甚至可能证明某个子程序满足强后置条件，但该子程序仍可能存在严重缺陷。这种出人意料的结果之所以出现，是因为后置条件的证明没有考虑不终止的可能性。子程序可能只是永远执行而不返回。一般来说，如果子程序包含无界递归，或者包含循环语句，就可能发生不终止。在本节中，我们研究如何证明子程序没有无限循环。

SPARK 子程序中有许多循环显然会终止，不需要特殊处理。例如，`for` 循环会在首次遇到循环时计算出的范围内遍历其循环参数。Ada 的规则不允许循环体修改循环参数，因此它只能在该指定值范围内前进。一旦循环参数耗尽这一范围，这类循环就保证会终止。不过，`while` 循环以及没有迭代方案而构造的循环（裸循环语句）可能执行的次数是不确定的。作为外层子程序正确性完整证明的一部分，证明这类循环会终止往往是可取甚至必要的。

可以借助 `Loop_Variant` pragma 来证明循环终止。`Loop_Variant` 的语义比我们目前见过的其他断言更复杂。`Loop_Variant` 允许你定义一个表达式，在循环执行过程中要么始终递增，要么始终递减。如果该表达式的值有合适的上界或下界，那么循环必然结束，因为表达式的值不可能无限递增或递减却不越过该界。表达式不允许在相邻循环迭代之间保持不变。表达式必须沿着单调方向“取得进展”逼近某个界。否则，循环可能永远执行。例如，`Loop_Variant` pragma

```
pragma Loop_Variant (Increases => A - B + C);
```

断言表达式 `A - B + C` 随循环的每次迭代而递增。

`Loop_Variant` pragma 允许指定多个表达式。每个表达式都以变化方向前缀修饰，方向为 `Increases` 或 `Decreases`。下面是一个使用整型变量 `X`、`Y` 和 `Z` 的示例：

```
pragma Loop_Variant (Increases => X, Decreases => Y - Z);
```

该断言表示：在每次循环迭代中，要么 `X` 的值递增，要么表达式 `Y - Z` 的值递减。当 pragma 中有多个表达式时，只要其他某个表达式按指定方向变化，任何特定表达式在特定迭代中都可以保持不变。

`Loop_Variant` pragma 中表达式的顺序很重要。在每次迭代中，会按文本顺序检查各表达式，直到发现某个表达式发生变化，或所有表达式都被检查完。如果最后检查的表达式按指定方向变化，则断言为真，否则为假。位于发生变化之后的所有表达式都会被忽略。因此，在我们的示例中，如果 `X` 递增，则不会考虑 `Y - Z` 发生了什么变化。

`Loop_Variant` pragma 中的表达式必须具有离散类型。任何离散类型的定义域都是有限的有序值集合。因此，离散类型的值会自动具有上界和下界。在我们的示例中，表达式的类型是 `Integer`，因此受 `Integer'First` 和 `Integer'Last` 约束。你无需再指定其他边界。

当然，循环不一定会让这些表达式一直变化到它们的边界。这一点并不重要。重要的是，边界必须存在，并且循环必须让这些表达式的值单调递增或递减。这足以证明循环最终必然终止。

与所有断言一样，循环变体在断言策略的控制下是可执行的。如果它们失败，就会像通常一样引发 `Assertion_Error`。同样，与所有断言一样，SPARK 工具会生成一个验证条件，以证明该变体永远不会失败。完成该验证条件的证明，也就证明了循环会终止。

在 6.4 节的 `Binary_Search` 示例中，该过程使用了一个裸循环语句，并在满足某些条件时通过 `exit` 语句结束循环。与 `for` 循环不同，这种形式的循环有可能无限执行。因此在这种情况下，宜使用 `Loop_Variant` 来证明这种情况不会发生。

要找到合适的循环变体，首先可以问：哪个表达式描述了循环正在取得的进展？在 `Binary_Search` 这个例子中，一种可能是 `High_Index` 和 `Low_Index` 始终彼此靠近：

`pragma Loop_Variant (Decreases => High_Index - Low_Index);`

如果循环的每次迭代都会缩小这两个索引之间的距离，那么循环最终会结束。

当这两个索引之差为零时，子程序将退出循环。不过，你可能会想：如果 `High_Index - Low_Index` 跳过零而变为负数，会发生什么？

在这种情况下，循环变体表达式的类型是 `Integer`（`Index_Type` 的基础类型）。理论上，`High_Index - Low_Index` 的最小可能值是 -99。当两个索引值分别位于各自的极端时，就可能出现这一值。如果循环真的是无限的，而循环变体却仍然成功，那么 `High_Index - Low_Index` 将永远递减下去。最终，当两个索引之一越界时，会引发 `Constraint_Error`；如果没有发生越界，
