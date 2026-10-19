

## 关于指针的通用技巧

对于许多类型的缺陷，定位错误是最容易的部分，而纠正它则是困难的部分。指针错误不同。指针错误通常是由于指针指向了不应该指向的地方。当你给一个错误的指针变量赋值时，你会将数据写入不应该写入的内存区域。这被称为“内存损坏”。有时内存损坏会产生可怕的、火爆的系统崩溃；有时它会改变程序另一部分计算的结果；有时会导致你的程序不可预测地跳过例程；有时它根本不会做任何事情。在最后一种情况下，指针错误是一个定时炸弹，等待在你向最重要的客户展示程序前五分钟毁掉你的程序。指针错误的症状往往与指针错误的原因无关。因此，纠正指针错误的大部分工作是定位原因。

成功使用指针需要双管齐下的策略。首先，避免一开始就引入指针错误。指针错误如此难以找到，以至于额外的预防措施是合理的。其次，尽可能在编码后尽快检测指针错误。指针错误的症状如此不稳定，以至于需要额外的措施使症状更可预测是合理的。以下是实现这些关键目标的方法：

![](img/649c8eee28c38ca1e062691e45dc9883_361_0.png)

- **将指针操作隔离在例程或类中** 假设你在程序的多个地方使用了一个链表。与其每次使用时都手动遍历列表，不如编写访问例程，如 `NextLink()`、`PreviousLink()`、`InsertLink()` 和 `DeleteLink()`。通过最大限度地减少访问指针的位置，你最大限度地减少了在程序中犯下粗心错误并花费永远时间寻找的可能性。由于代码与数据实现细节相对独立，你也有更大的机会在其他程序中重用它。编写指针分配的例程是集中控制你的数据的另一种方式。

- **同时声明和定义指针** 在声明变量附近为其分配初始值通常是良好的编程实践，而在处理指针时它更有价值。以下是不该做的示例：

![](img/649c8eee28c38ca1e062691e45dc9883_361_1.png)

**C++ 坏指针初始化示例**

```cpp
Employee *employeePtr;
// lots of code
...
employeePtr = new Employee;
```

- 2. 将前 4 个字节设置为狗牌值，然后返回指向其后内存的指针。

![](img/649c8eee28c38ca1e062691e45dc9883_363_0.png)

- 3. 当需要删除指针时，检查标签。

![](img/649c8eee28c38ca1e062691e45dc9883_363_1.png)

- 4. 如果标签正常，将其设置为 0 或其他你和你的程序识别为无效标签值的值。你不希望该值在内存被释放后被误认为有效标签值。出于同样的原因，将数据设置为 0、0xCC 或其他非随机值。

- 5. 最后，删除指针。

![](img/649c8eee28c38ca1e062691e45dc9883_363_2.png)

在你分配的内存块开头放置一个狗牌，允许你在无需维护已分配内存块列表的情况下检查对内存块重复释放的尝试。在内存块末尾放置狗牌允许你检查是否覆盖了超出预期使用位置的内存。你可以在块的开头和结尾使用标签来实现这两个目标。

你可以将这种方法与前面建议的合理性检查结合使用——检查指针是否在 StartData 和 EndData 之间。为了确保指针指向合理的位置，而不是检查可能的内存范围，检查指针是否在已分配指针的列表中。

你可以在删除变量前只检查一次标签字段。损坏的标签就会告诉你，在该变量的生命周期中，其内容在某个时间点被损坏了。然而，你检查标签字段的次数越多，就越接近问题的根源检测到损坏。

- **添加显式冗余** 使用标签字段的替代方案是重复使用某些字段。如果冗余字段中的数据不匹配，你就知道内存已被损坏。如果直接操作指针，这可能会导致大量开销。然而，如果你在例程中隔离指针操作，它只会在少数地方增加重复代码。

- **为清晰使用额外的指针变量** 绝对不要吝啬指针变量。其他地方也提到，变量不应用于多个目的。对于指针变量尤其如此。弄清楚某人对链表做了什么已经够难了，还要弄清楚为什么一个通用的 genericLink 变量被反复使用，或者 pointer->next->last->next 指向什么。考虑以下代码片段：

**C++ 传统节点插入代码示例**

```cpp
void InsertLink(
    Node *currentNode,
    Node *insertNode
) {
    // insert "insertNode" after "currentNode"
    insertNode->next = currentNode->next;
    insertNode->previous = currentNode;
    if ( currentNode->next != NULL ) {
        currentNode->next->previous = insertNode;
    }
    currentNode->next = insertNode;
}
```

这一行是不必要地难以理解。

这是插入链表节点的传统代码，理解起来不必要地困难。插入新节点涉及三个对象：当前节点、当前节点之后当前跟随的节点，以及要插入它们之间的节点。代码片段明确承认只有两个对象：insertNode 和 currentNode。它迫使你弄清楚并记住 currentNode->next 也参与其中。如果你试图在不使用当前节点原本跟随的节点的情况下绘制正在发生的事情，你会得到类似这样的结果：

![](img/649c8eee28c38ca1e062691e45dc9883_364_0.png)

更好的图示会识别所有三个对象。它看起来像这样：

![](img/649c8eee28c38ca1e062691e45dc9883_364_1.png)

以下是明确引用涉及的三个对象的代码：

**C++ 更易读的节点插入代码示例**

```cpp
void InsertLink(
    Node *startNode,
    Node *newMiddleNode
) {
    // insert "newMiddleNode" between "startNode" and "followingNode"
    Node *followingNode = startNode->next;
    newMiddleNode->next = followingNode;
    newMiddleNode->previous = startNode;
    if ( followingNode != NULL ) {
        followingNode->previous = newMiddleNode;
    }
    startNode->next = newMiddleNode;
}
```

这段代码片段多了一行代码，但没有第一个片段的 `currentNode->next->previous`，更容易跟随。

- **简化复杂的指针表达式** 复杂的指针表达式难以阅读。如果你的代码包含像 p->q->r->s.data 这样的表达式，想想必须阅读该表达式的人。以下是一个特别糟糕的例子：

**C++ 难以理解的指针表达式示例**

```cpp
for ( rateIndex = 0; rateIndex < numRates; rateIndex++ ) {
    netRate[ rateIndex ] = baseRate[ rateIndex ] * rates->discounts->factors->net;
}
```

像本例中指针表达式这样复杂的表达式会导致代码必须被推敲而不是被阅读。如果你的代码包含复杂表达式，将其赋给一个命名良好的变量以阐明操作的意图。以下是改进后的示例版本：

**C++ 简化复杂指针表达式示例**

```cpp
quantityDiscount = rates->discounts->factors->net;
for ( rateIndex = 0; rateIndex < numRates; rateIndex++ ) {
    netRate[ rateIndex ] = baseRate[ rateIndex ] * quantityDiscount;
}
```

通过这种简化，你不仅获得了可读性的提升，而且可能还会在循环内简化指针操作时获得性能提升。像往常一样，你必须在押上任何钱之前测量性能收益。

- **画一张图** 指针的代码描述会变得令人困惑。通常画一张图会有所帮助。例如，链表插入问题的图可能看起来像图 13-2 所示。

**交叉引用** 图 13-2 中的图示可以成为你程序外部文档的一部分。有关良好文档实践的详细信息，请参阅第 32 章“自文档化代码”。

![](img/649c8eee28c38ca1e062691e45dc9883_365_0.png)

**图 13-2** 一个有助于我们思考重新链接指针所涉及步骤的图片示例。

