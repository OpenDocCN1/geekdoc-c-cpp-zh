

编写一个程序，使用节点和指针实现迷宫。图中的每个节点都将对应于以类或结构体形式实现的你代码中的一个节点。边对应于从一个节点指向另一个节点的双向链接。将用户置于节点 A。用户的目标是到达节点 L 的终点。程序应输出可能的向北、向南、向东或向西移动方向。示例执行如下所示。

你位于迷宫的 A 房间，里面有许多曲折的小通道，都很相似。
你可以向 (E)东、(S)南或 (Q)退出。
E

你位于迷宫的 B 房间，里面有许多曲折的小通道，都很相似。
你可以向 (W)西、(S)南或 (Q)退出。
S

你位于迷宫的 F 房间，里面有许多曲折的小通道，都很相似。
你可以向 (E)东、(N)北或 (Q)退出。
E

## 10. 编写一个程序，使用另外两个栈对一组整数值进行重新排列和排序。以下算法描述了如何实现此操作：

+   1. 从名为 primary 的数字栈和两个空栈 lower 和 higher 开始。
+   2. 从 primary 栈弹出第一个数字并将其放入 lower 栈
+   3. 从 primary 栈弹出下一个数字，如果它小于你之前放入 lower 栈的数字，则将其添加到 lower 栈，否则将其放入 higher 栈。
+   4. 重复步骤 3 直到 primary 栈为空。
+   5. 弹出 lower 栈中的每个元素并将其重新添加回 primary 栈。
+   6. 弹出 higher 栈的每个元素。如果该值大于 primary 栈头部的值，则将其添加到 primary 栈，否则将该数字添加到 lower 栈。
+   7. 从步骤 3 重复到步骤 6 的过程，直到 higher 和 lower 栈均不包含元素。此时，primary 栈将被排序。

提示：使用第 13.17 和 13.19 节中给出的栈类实现作为设计栈数据类型的起点。

## 11. 编写一个双向链表类以在 Node 对象中存储 double 值。包含以下功能：

+   - 在前端和后端插入的函数
+   - 返回第一个和最后一个元素值的函数
+   - 以正向和反向打印列表的函数
+   - 删除第一个元素和最后一个元素的函数
+   - 检查列表是否包含某个元素的函数
+   - 清空整个列表的函数
+   - 检查列表是否为空的函数
+   - 返回列表大小的函数

通过在前端和后端添加元素来测试你的类，以正向和反向打印列表并删除元素。有许多可能的边界情况需要检查，例如删除列表中的最后一个元素或打印空列表。考虑其他测试用例以检查双向链表的完整功能。确保你的双向链表类和 Node 类仔细处理动态内存并且不泄漏内存。

本页 intentionally left blank

![](img/88b1f375f11336dbd9dac8b1675d0698_825_0.png)

# Recursion 14

+   **14.1 RECURSIVE FUNCTIONS FOR TASKS** 825
+   
+   *Case Study:* Vertical Numbers 825
+   
+   A Closer Look at Recursion 831
+   
+   *Pitfall:* Infinite Recursion 833
+   
+   Stacks for Recursion 834
+   
+   *Pitfall:* Stack Overflow 836
+   
+   Recursion Versus Iteration 836

+   **14.2 RECURSIVE FUNCTIONS FOR VALUES** 838
+   
+   General Form for a Recursive Function That Returns a Value 838
+   
+   *Programming Example:* Another Powers Function 838

+   **14.3 THINKING RECURSIVELY** 843
+   
+   Recursive Design Techniques 843
+   
+   *Case Study:* Binary Search—An Example of Recursive Thinking 844
+   
+   *Programming Example:* A Recursive Member Function 852

+   Chapter Summary 856
+   
+   Answers to Self-Test Exercises 856

+   Practice Programs 861
+   
+   Programming Projects 861

![](img/88b1f375f11336dbd9dac8b1675d0698_826_0.png)

在一次关于宇宙学和太阳系结构的讲座后，威廉·詹姆斯被一位小老太太拦住。
“你关于太阳是太阳系中心、地球是围绕其旋转的球体的理论听起来很有说服力，詹姆斯先生，但它是错误的。我有一个更好的理论，”小老太太说。
“那是什么，夫人？”詹姆斯礼貌地问道。
“我们生活在巨龟背上的地球地壳上。”
不愿通过大量科学证据来摧毁这个荒谬的小理论，詹姆斯决定通过让对手看到其立场的不足来温和地劝阻她。
“如果你的理论正确，夫人，”他问道，“这只乌龟站在什么上面？”
“你是个很聪明的人，詹姆斯先生，这是一个很好的问题，”小老太太回答道，“但我对此有一个答案。那就是：第一只乌龟站在第二只、更大得多的乌龟背上，后者正好在它下方。”
“但这第二只乌龟站在什么上面？”詹姆斯耐心地追问。
对此，小老太太得意地叫道。“没用，詹姆斯先生——一直都是乌龟。”

J. R. R. TOLLKIEN, Constraints on Variables in Syntax

# INTRODUCTION

你已经遇到了一些循环定义的情况，结果令人满意。最突出的例子是某些 C++ 语句的定义。例如，while 语句的定义说它可以包含其他（更小的）语句。由于这些更小语句的可能性之一是另一个 while 语句，因此该定义中存在一种循环性。while 语句的定义，如果写成完整细节，将包含对 while 语句的引用。在数学中，这种循环定义称为递归定义。在 C++ 中，函数可以以同样的方式用自身来定义。更精确地说，函数定义可能包含对自身的调用。在这种情况下，函数被称为递归。本章讨论 C++ 中的递归，以及更一般地将递归作为编程和问题解决技术。

# PREREQUISITES

第 14.1 和 14.2 节仅使用第 2 章到第 5 章的材料。第 14.3 节使用第 2 章到第 7 章和第 10 章的材料。

## 14.1 RECURSIVE FUNCTIONS FOR TASKS

> 我还记得《一千零一夜》中那个夜晚，当时谢赫拉查德（由于抄写员的一个神奇疏忽）开始逐字逐句地讲述《一千零一夜》的故事，从而冒着再次来到她必须重复它的那个夜晚的风险，并由此走向无限。

JORGE LUIS BORGES, The Garden of Forking Paths

当你编写一个函数来解决一个任务时，一个基本的设计技术是将任务分解为子任务。有时会出现至少一个子任务是同一任务的较小示例的情况。例如，如果任务是在数组中搜索特定值，你可能会将其分为搜索数组前半部分的子任务和搜索数组后半部分的子任务。搜索数组半部分的子任务是“更小”的原始任务版本。每当一个子任务是原始任务的较小版本时，你就可以使用递归函数来解决原始任务。需要一点训练才能轻松地以这种方式分解问题，但一旦你学会了这种技术，它可以成为设计算法、最终是 C++ 函数的最快方法之一。我们从一个简单的案例研究开始来说明这种技术。

# Recursion

在 C++ 中，函数定义可能包含对正在定义的函数的调用。在这种情况下，函数被称为递归。

## CASE STUDY Vertical Numbers

在本案例研究中，我们设计一个递归的 void 函数，将数字写到屏幕上，数字以垂直方式书写，使得例如 1984 将被写成

![](img/88b1f375f11336dbd9dac8b1675d0698_827_0.png)

# Problem Definition

我们函数的声明和头部注释如下：

```
void writeVertical(int n);
//Precondition: n >= 0.
//Postcondition: The number n is written to the screen
//vertically with each digit on a separate line.
```
