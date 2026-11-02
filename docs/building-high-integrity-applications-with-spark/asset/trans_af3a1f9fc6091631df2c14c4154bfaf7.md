
### 9.1.2 Ghost 变量

方面 Ghost 既可以应用于变量和常量，也可以应用于函数。此类变量只能用于验证断言中。它们通常用于循环不变式中。与 Ghost 函数一样，有效程序的运行时行为无论是否包含 Ghost 变量都相同。我们将在下一节中查看一个包含 Ghost 变量和常量的示例。

## 9.2 传递性质的证明

我们需要证明的许多性质都是传递关系。作为此类性质以及 Ghost 实体用法的一个示例，我们回到选择排序过程。我们在第1.4节给出了它的规范，并在此重复：

```
pragma SPARK_Mode (On);
package Sorters is

    type Array_Type is array ( Positive range <> ) of Integer;

    function Perm (A : in Array_Type;
                   B : in Array_Type) return Boolean
    -- Returns True if A is a permutation of B
    with Global => null,
         Ghost => True,
         Import => True;

    procedure Selection_Sort (Values : in out Array_Type)
    -- Sorts the elements in the array Values in ascending order
    with Depends => (Values => Values),
         Pre => Values'Length >= 1 and
                Values'Last <= Positive'Last,
         Post => (for all J in Values'First .. Values'Last - 1 =>
                  Values (J) <= Values (J + 1)) and then
                Perm (Values'Old, Values);
end Sorters;
```

过程 Selection_Sort 有两个后置条件。第一个后置条件指出返回的值按升序排列。第二个后置条件使用 Ghost 函数 Perm 指出返回的数组 Values 是原数组 Values'Old 的一个排列。也就是说，新数组是原数组中值的重新排序。如果没有这第二个后置条件，一个给定整数 (5, 7, 3, 3, 8) 并返回 (5, 5, 5, 5, 5) 的排序过程将会是有效的。

判断两个数组是否互为排列的一种常见方法是对每个数组进行排序，并比较排序后的数组。由于我们正在使用排列性质来验证排序过程，因此不能使用排序来验证排列。另一种方法是统计每个数组中每个元素的数量，并比较这些计数。由于我们的数组分量是整数，对于32位整数表示，这种方法可能需要 2³² 个计数器。

我们采用另一种方法来表明结果是原数组的一个排列。函数 Perm 是一个 Ghost 函数。方面 Import 指出该函数的函数体位于 SPARK 程序外部。我们不会编写函数体，而是向证明工具提供验证排列后置条件所需的数学规则。以下是实现我们的选择排序的完整包体：

```
pragma SPARK_Mode (On);
package body Sorters is

function Perm_Transitive (A, B, C : Array_Type) return Boolean
  with Global => null,
    Post => (if Perm_Transitive'Result
        and then Perm (A, B)
        and then Perm (B, C)
        then Perm (A, C)),
    Ghost => True,
    Import => True;

procedure Swap (Values : in out Array_Type;
    X : in Positive ;
    Y : in Positive )
  with Depends => (Values => (Values, X, Y)),
    Pre => (X in Values'Range and then
        Y in Values'Range and then
        X /= Y),
    Post => Perm (Values'Old, Values)  and then
        (Values (X) = Values'Old (Y) and then
        Values (Y) = Values'Old (X) and then
        (for all J in Values'Range =>
        (if J /= X and J /= Y then Values (J) = Values'Old (J))))
is
  Values_Old : constant Array_Type := Values
    with Ghost => True;
  Temp : Integer;
begin
    Temp := Values (X);
    Values (X) := Values (Y);
    Values (Y) := Temp;
    pragma Assume (Perm (Values_Old, Values));
end Swap;

-- Finds the index of the smallest element in the array
function Index_Of_Minimum (Unsorted : in Array_Type) return Positive
    with Pre => Unsorted'First <= Unsorted'Last,
         Post => Index_Of_Minimum'Result in Unsorted'Range and then
                 (for all J in Unsorted'Range =>
                    Unsorted (Index_Of_Minimum'Result) <= Unsorted (J))
is
    Min : Positive ;
begin
    Min := Unsorted'First ;
    for Index in Unsorted'First .. Unsorted'Last loop
        pragma Loop_Invariant
            (Min in Unsorted'Range and then
             (for all J in Unsorted'First .. Index - 1 =>
                Unsorted (Min) <= Unsorted (J)));
        if Unsorted (Index) < Unsorted (Min) then
            Min := Index;
        end if;
    end loop;
    return Min;
end Index_Of_Minimum;

procedure Selection_Sort (Values : in out Array_Type) is
    Values_Last : Array_Type (Values'Range)
        with Ghost => True;
    Smallest : Positive ;  -- Index of the smallest value in the unsorted part
begin  -- Selection_Sort
    pragma Assume (Perm (Values, Values));
    for Current in Values'First .. Values'Last - 1 loop
        Values_Last := Values;
        Smallest := Index_Of_Minimum (Values (Current .. Values'Last));
        if Smallest /= Current then
            Swap (Values => Values,
                  X      => Current,
                  Y      => Smallest);
        end if;

        pragma Assume (Perm_Transitive (Values'Loop_Entry, Values_Last, Values));

        pragma Loop_Invariant (Perm (Values'Loop_Entry, Values));
        pragma Loop_Invariant  -- Simple partition property
          ((for all J in Current .. Values'Last =>
               Values (Current) <= Values (J)));
        pragma Loop_Invariant  -- order property
          ((for all J in Values'First .. Current =>
               Values (J) <= Values (J + 1)));
    end loop;
end Selection_Sort;
end Sorters;
```

排列验证的核心位于从第14行开始的过程 Swap 中。它的后置条件指出：(1) 结果数组是原数组的一个排列；(2) 索引位置 X 和 Y 处的值已被交换；(3) 数组中其余的值保持不变。

我们知道，交换数组中的两个元素会生成原数组的一个排列。然而，SPARK 工具并不知道这一事实。我们在第34行使用 pragma Assume 和 Ghost 函数 Perm 来陈述这一事实。交换两个元素后，SPARK 工具将假定结果是原数组的一个排列。我们使用 Ghost 常量 Values_Old 保存原数组的副本。我们不能使用 Values'Old，因为 'Old 属性只能用于后置条件中。²

接下来，我们必须告诉 SPARK 工具：经过多次元素交换后，最终数组是原数组的一个排列。这是一个传递性质：如果 A 和 B 互为排列，且 B 和 C 互为排列，那么 A 和 C 互为排列。我们使用另一个定义在第4–11行的 Ghost 函数 Perm_Transitive 来表达这种传递性。该函数的后置条件陈述了传递性质。函数后置条件应始终提及函数的结果，因此我们也包含了它。由于后置条件就是我们证明所需的全部内容，我们包含了方面 Import，这样就不必为该函数编写函数体。

第78行的 pragma Assume 告诉证明工具：每次交换后，结果仍然是原数组的一个排列。此 pragma 中对 Perm_Transitive 的调用的三个参数分别是原数组（其在循环开始之前的值）、最后一次交换之前的数组，以及当前数组。我们使用 Ghost 变量 Values_Last 保存交换元素之前的数组副本。

还有一项事实需要提供给证明工具：数组是其自身的一个排列。这一事实在第67行的 pragma Assume 中给出。

像往常一样，我们需要通过为循环编写不变式来帮助证明工具证明我们的后置条件。虽然每个循环只能编写一个不变式，但只要多个 Loop_Invariant pragma 是连续的，就可以使用它们。第80–86行的三个 pragma 可以使用合取运算符 and then 写成单个 pragma，就像在函数 Index_Of_Minimum 中所做的那样。请注意 Selection_Sort 和 Index_Of_Minimum 中的循环不变式如何支持它们的后置条件。

本示例中采用的方法可以应用于任何需要传递性质的证明。让我们看一个更通用的示例。在规范中，

- 将该具有传递性的性质声明为没有函数体的 Ghost 函数，并且
- 在你希望证明其保持该性质的修改操作的后置条件中使用该性质。

看看你能否在我们的排序包规范（第330页）中找出这两个步骤。

在包体中，

- 将传递关系声明为没有函数体的 Ghost 函数（参见排序包体的第4–11行），
- 在修改操作体的开头添加 pragma Assume，以陈述该性质适用于自身（参见排序包体的第67行），
- 声明一个 Ghost 变量（参见排序包体的第63–64行），并在应用修改之前将当前值赋给它（参见第69行），以及
- 在执行修改后添加带有传递关系 Ghost 函数的 pragma Assume，以指示该性质适用于当前值（参见排序包体的第78行）。

让我们看一个说明此方法的更简单示例。³ 过程 Change 对其参数 X 进行一些修改，其后置条件是由函数 Property 给出的传递性质成立。

```
package Transitive
with SPARK_Mode => On
is
    function Property (X, Y : in Natural) return Boolean
    with Global => null,
```
