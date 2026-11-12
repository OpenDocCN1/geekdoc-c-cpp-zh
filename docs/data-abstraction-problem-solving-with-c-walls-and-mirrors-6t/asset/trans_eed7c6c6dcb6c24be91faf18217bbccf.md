
13. 使用图 6-10 中的地图（参见检查点问题 8）执行 HPAir 算法，处理以下请求。显示每个步骤后栈的状态。

- a. 从 A 飞往 F。
- b. 从 A 飞往 G。
- c. 从 F 飞往 H。
- d. 从 D 飞往 A。
- e. 从 I 飞往 G。

14. 第 5 章第 5.1.2 节定义了“回文”。编写一个使用栈来测试给定字符串是否为回文的伪代码算法。

15. 你可以使用栈的公理来证明，由以下操作序列定义的栈

```
Create an empty stack
Push a 5
Push a 7
Push a 3
Pop (the 3)
Push a 9
Pop (the 9)
Push a 4
Pop (the 4)
```

可以写成

```
((((((new Stack()).push(5)).push(7)).push(3)).pop()).push(9)).push(4)).pop()
```

与由以下序列定义的栈完全相同

```
Create an empty stack
Push a 5
Push a 7
Push a 9
Push a 9
```

可以写成

```
((new Stack()).push(5)).push(7)).push(9)
```

同样，你可以使用公理来证明

```
((((((new Stack()).push(1)).push(2)).pop()).push(3)).pop()).pop()).isEmpty()
```

为真。

- a. 将栈表示为不含任何 pop 操作的 push 操作序列的以下形式称为规范形式：

```
( ... (new Stack()).push()).push())... ).push()
```

证明任何栈都等于一个规范形式的栈。

- b. 证明规范形式是唯一的。也就是说，一个栈只等于一个规范形式的栈。

- c. 使用公理正式证明

```
(((((((new Stack()).push(6)).push(9)).pop()).pop()).push(2)).pop()).push(3)).push(((pop()).peek()
```

等于 3。

## 编程问题

- 1. 使用标准模板库中的类 stack，定义并测试从 StackInterface 派生的类 OurStack，如清单 6-1 所示。类 stack 具有以下方法，你可以使用它们来定义 OurStack 的方法。

```
stack(); // Default constructor
bool empty() const; // Tests whether the stack is empty
ItemType& top(); // Returns a reference to the top of the stack
void push(const ItemType& newEntry); // Adds newEntry to the top of the stack
void pop(); // Removes the top of the stack
```

为避免 pop，请使用以下 include 语句：

`#include <stack>`

在以下任何问题中需要栈时，请使用编程问题 1 要求你编写的类 OurStack。

- 2. 实现练习 7 中扩展的平衡括号问题的解决方案。

- 3. 编写一个使用栈来测试给定字符串是否为回文的函数。练习 14 要求你为这样的函数编写算法。

- 4. 第 6.2.2 节描述了语言

L = {s$'：s 是可能为空的、不包含 $ 的字符串，s' = reverse(s)}

的识别算法。实现此算法。

- 5. 设计一个后缀计算器类。使用本章给出的算法来计算输入到计算器中的后缀表达式。仅使用运算符 +、-、* 和 /。假设后缀表达式在语法上是正确的。

- 6. 考虑由单个数字操作数、运算符 +、-、* 和 / 以及括号组成的简单中缀表达式。假设一元运算符非法，且表达式中不包含嵌入空格。设计并实现一个中缀计算器类。使用本章给出的算法来计算输入到计算器中的中缀表达式。你必须先将中缀表达式转换为后缀形式，然后计算得到的后缀表达式。

- 7. 本章描述的中缀转后缀转换算法假设给定的中缀表达式在语法上是正确的。在不做此假设的情况下修改编程问题 6。

- 8. 重复编程问题 6，但使用以下算法来计算中缀表达式 infixExp。该算法使用两个栈：一个栈 opStack 包含运算符，另一个栈 valStack 包含操作数和中间结果的值。注意，该算法将括号视为优先级最低的运算符。

```
for (each character ch in infixExp)
{
    switch (ch)
    {
        case ch is an operand, that is, a digit
            valStack.push(ch)
            break
        case ch is a '('
            opStack.push(ch)
            break
        case ch is an operator
            if (opStack.isEmpty())
                opStack.push(ch)
            else if (precedence(ch) > precedence(opStack.peek()))
                opStack.push(ch)
            else
                while (!opStack.isEmpty() and
                       precedence(ch) <= precedence(opStack.peek()))
                    Execute
                    opStack.push(ch)
                }
            break
        case ch is a ')'
            while (opStack.peek() is not a '(')
                Execute
                opStack.pop()
            break
    }
}
while (!opStack.isEmpty())
    Execute
result = valStack.peek()
```

注意，Execute 表示：

```
operand2 = valStack.peek()
valStack.pop()
operand1 = valStack.peek()
valStack.pop()
op = opStack.peek()
opStack.pop()
result = operand1 op operand2
valStack.push(result)
```

为你的实现选择以下两种方法之一：

- 运算符栈 opStack 包含字符，但操作数栈 valStack 包含整数。
- 栈 opStack 包含表示运算符的整数代码，因此两个栈都包含整数。

- 9. 编程问题 8 给出的中缀求值算法假设给定的中缀表达式在语法上是正确的。在不做此假设的情况下重复编程问题 8。

- 10. 使用栈，编写第 2 章中定义的函数 solveTowers 的非递归版本。

- 11. 完成 HPAir 问题的解决方案。程序的输入由三个文本文件组成，如下所示：

| cityFile | 每行包含 HPAir 服务的一个城市的名称。名称按字母顺序排列。 |
| --- | --- |
| flightFile | 每行包含一对城市名称，表示 HPAir 的一个航班的出发地和目的地。 |
| requestFile | 每行包含一对城市名称，表示从某个出发地飞往某个目的地的请求。 |

你可以做出以下假设：

- 每个城市名称最多包含 15 个字符。城市名称对之间用逗号分隔。
- HPAir 最多服务 20 个城市。
- 输入数据是正确的。

例如，输入文件可能如下所示：

```
cityFile:             Albuquerque
                              Chicago
                              San Diego

flightFile:           Chicago,      San Diego
                              Chicago,      Albuquerque
                              Albuquerque,  Chicago

requestFile:          Albuquerque,  San Diego
                              Albuquerque,  Paris
                              San Diego,    Chicago
```

对于此输入，程序应产生以下输出：

```
Request is to fly from Albuquerque to San Diego.
HPAir Flies from Albuquerque to San Diego.

Request is to fly from Albuquerque to Paris.
Sorry. HPAir does not serve Paris.

Request is to fly from San Diego to Chicago.
Sorry. HPAir does not fly from San Diego to Chicago.
```

首先，将 ADT 航班图实现为 C++ 类 Map。使用 isPath 的栈版本。因为 getNextCity 是搜索算法在航班图上执行的主要操作，你应该选择一种能够高效确定哪些城市与给定城市相邻的实现。如果有 n 个城市，编号为 1、2、..., n，你可以使用 n 个链接节点链来表示航班图。当且仅当从城市 i 到城市 j 存在有向路径时，才在列表 i 上为城市 j 放置一个节点。这种数据结构称为邻接表，图 6-14 说明了图 6.6 中航班图的邻接表。第 20 章在介绍图的表示方法时进一步讨论了邻接表。届时，你将了解为什么邻接表是当前程序的一个好选择。

为简化输入文本文件的读取，定义一个包含以下方法的类：

```
// Returns a name from the next line in a text file.
//+getName(): string

// Returns a pair of two names from the next line in a text file.
//+getNamePair(): Pair
```

- 12. 在 HPAir 问题的实现中（参见前一个编程问题），查找与城市 i 相邻的下一个未访问城市的搜索始终从邻接表中第 i 个链的开头开始。这种方法实际上有点低效，因为一旦搜索访问了一个城市，该城市就永远不会变成未访问状态。修改程序，使查找下一个城市的搜索从上次搜索结束的地方开始。也就是说，维护一个指向邻接表的尝试下一个指针数组。
