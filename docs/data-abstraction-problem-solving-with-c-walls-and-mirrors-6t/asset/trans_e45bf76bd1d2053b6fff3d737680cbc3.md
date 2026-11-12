

## 10.2 衡量算法的效率

Well-designed algorithms reduce the human costs of implementing the algorithm with a program, of maintaining the program, and of modifying the program. Developing good problem-solving skills and programming style has been and continues to be important. However, the efficiency of algorithms is also important. Efficiency is a criterion that you should consider when selecting an algorithm and its implementation.
设计良好的算法能降低用程序实现算法、维护程序以及修改程序的人力成本。培养良好的问题解决能力和编程风格过去重要，现在依然重要。然而，算法的效率同样重要。在选择算法及其实现时，效率是你应该考虑的一个标准。

### VideoNote Measuring algorithmic efficiency
### VideoNote 衡量算法效率

The comparison of algorithms is a topic central to computer science. Measuring an algorithm's efficiency is quite important because your choice of algorithm for a given application often has a great impact. Responsive word processors, grocery checkout systems, automatic teller machines, video games, and life support systems all depend on efficient algorithms.
算法比较是计算机科学的核心主题。衡量算法的效率非常重要，因为你为特定应用选择的算法往往会产生重大影响。响应迅速的文字处理器、超市结账系统、自动取款机、视频游戏和生命支持系统都依赖于高效算法。

### Consider efficiency when selecting an algorithm
### 选择算法时考虑效率

The analysis of algorithms is the area of computer science that provides tools for contrasting the efficiency of different algorithms. Notice the use of the term "algorithms" rather than "programs"; it is important to emphasize that the analysis concerns itself primarily with significant differences in efficiency—differences that you can usually obtain only through superior algorithms and rarely through clever tricks in coding. Reductions in computing costs due to clever coding tricks are often more than offset by reduced program readability, which increases human costs. An analysis should focus on gross differences in the efficiency of algorithms that are likely to dominate the overall cost of a solution. To do otherwise could lead you to select an algorithm that runs a small fraction of a second faster than another algorithm yet requires many more hours of your time to implement and maintain.
算法分析是计算机科学中用于对比不同算法效率的工具所在的领域。请注意使用“算法”而非“程序”这一术语；重要的是要强调，分析主要关注效率上的显著差异——这些差异通常只能通过更优的算法获得，而很少通过代码中的巧妙技巧获得。由于巧妙编码技巧带来的计算成本降低，往往会被程序可读性降低所抵消，而可读性降低会增加人力成本。分析应关注算法效率上的显著差异，这些差异可能会主导解决方案的总成本。否则，可能会导致你选择一个比另一个算法快几分之一秒，但实现和维护却需要多出许多小时的算法。

### A comparison of algorithms should focus on significant differences in efficiency
### 算法比较应关注效率上的显著差异

The efficient use of both time and memory is important. Computer scientists use similar techniques to analyze an algorithm's time and space efficiency. As none of the algorithms covered in this text has significant space requirements, our focus is primarily on time efficiency.
时间和内存的高效利用都很重要。计算机科学家使用类似的技术来分析算法的时间效率和空间效率。由于本文涵盖的算法都没有显著的空间需求，我们的重点主要放在时间效率上。

How do you compare the time efficiency of two algorithms that solve the same problem? One possible approach is to implement the two algorithms and run the programs. This approach has at least three fundamental problems:
如何比较解决同一问题的两个算法的时间效率？一种可能的方法是实现这两个算法并运行程序。这种方法至少有三个根本性问题：

### Three difficulties with comparing programs instead of algorithms
### 比较程序而非算法的三个困难

- How are the algorithms coded? If algorithm A1 runs faster than algorithm A2, it could be the result of better programming. Thus, if you compare the running times of the programs, you are really comparing implementations of the algorithms rather than the algorithms themselves. You should not compare implementations, because they are sensitive to factors such as programming style that tend to cloud the issue of which algorithm is inherently more efficient.
- 算法是如何编码的？如果算法 A1 运行得比算法 A2 快，这可能是更好编程的结果。因此，如果你比较程序的运行时间，你实际上是在比较算法的实现而非算法本身。你不应该比较实现，因为它们对编程风格等因素敏感，这些因素往往会模糊哪个算法本质上更高效的问题。
- What computer should you use? The particular operations that the algorithms require can cause A1 to run faster than A2 on one computer, while the opposite is true on another computer. You should compare the efficiency of the algorithms independently of a particular computer.
- 应该使用什么计算机？算法所需的特定操作可能导致 A1 在一台计算机上比 A2 运行得更快，而在另一台计算机上则相反。你应该独立于特定计算机来比较算法的效率。
- What data should the programs use? Perhaps the most important difficulty on this list is the selection of the data for the programs to use. There is always the danger that you could select instances of the problem for which one of the algorithms runs uncharacteristically fast. For example, when comparing a sequential search and a binary search of a sorted array, you might search for an item that happens to be the smallest item in the array. In such a case, the sequential search finds the item more quickly than the binary search because the item is first in the array and is thus the first item that the sequential search examines. Any analysis of efficiency must be independent of specific data.
- 程序应该使用什么数据？也许这个列表中最重要的困难是为程序选择要使用的数据。总存在这样的危险：你可能会选择问题的实例，使得其中一个算法运行得不寻常地快。例如，在比较有序数组的顺序查找和二分查找时，你可能会搜索一个碰巧是数组中最小项的项目。在这种情况下，顺序查找比二分查找更快地找到该项目，因为该项目在数组中排第一，因此是顺序查找检查的第一个项目。任何效率分析都必须独立于特定数据。

### Algorithm analysis should be independent of specific implementations, computers, and data
### 算法分析应独立于特定实现、计算机和数据

To overcome these difficulties, computer scientists employ mathematical techniques that analyze algorithms independently of specific implementations, computers, or data. You begin this analysis by counting the number of significant operations in a particular solution, as the next section describes.
为了克服这些困难，计算机科学家采用数学技术，独立于特定实现、计算机或数据来分析算法。你通过计算特定解决方案中的重要操作数量来开始此分析，如下一节所述。

> Note: In general, you should avoid analyzing an algorithm solely by studying the running times of a specific implementation. Running times are influenced by such factors as programming style, the particular computer, and the data on which the program is run.
> 注：一般来说，你应避免仅通过研究特定实现的运行时间来分析算法。运行时间受编程风格、特定计算机以及程序运行的数据等因素的影响。

### 10.2.1 The Execution Time of Algorithms
### 10.2.1 算法的执行时间

### Counting an algorithm's operations is a way to assess its efficiency
### 计算算法的操作是评估其效率的一种方法

Previous chapters have informally compared different solutions to a given problem by looking at the number of operations that each solution required. For example, Chapter 4 compared array-based and link-based implementations of the ADT Bag. An array-based bag can access its ith item directly in one step, because the item is stored in items[i-1]. A link-based bag, however, must traverse a chain of linked nodes from its beginning until the ith node is reached and would therefore require i steps.
前几章非正式地比较了给定问题的不同解决方案，方法是查看每个解决方案所需的操作数量。例如，第 4 章比较了基于数组和基于链表的 ADT Bag 实现。基于数组的 bag 可以在一步内直接访问其第 i 个项，因为该项存储在 items[i-1] 中。然而，基于链表的 bag 必须从链表链节点链的开头开始遍历，直到到达第 i 个节点，因此需要 i 步。

An algorithm’s execution time is related to the number of operations it requires. This is usually expressed in terms of the number, n, of items the algorithm must process. Counting an algorithm’s operations—if possible—is a way to assess its efficiency. Let’s consider a few other examples.
算法的执行时间与其所需的操作数量相关。这通常用算法必须处理的项目数 n 来表示。计算算法的操作（如果可能）是评估其效率的一种方法。让我们考虑几个其他示例。

### Traversal of linked nodes
### 遍历链表链节点

As an example of traversing a chain of linked nodes, consider displaying the data in such a chain. If headPtr points to the first node in the chain, the following C++ statements display its data:
作为遍历链表链节点链的示例，考虑显示此类链中的数据。如果 headPtr 指向链中的第一个节点，以下 C++ 语句显示其数据：

```cpp
Node<ItemType>* curPtr = headPtr;
while (curPtr != nullptr)
{
    cout << curPtr->getItem() << endl;
    curPtr = curPtr->getNext();
} // end while
```

### Displaying the data in a linked chain of n nodes requires time proportional to n
### 显示 n 个节点的链表链中的数据所需时间与 n 成正比

If we have n nodes, these statements require n + 1 assignments, n + 1 comparisons, and n write operations. If each assignment, comparison, and write operation requires, respectively, a, c, and w time units, the statements require (n + 1) × (a + c + n × w) time units. Thus, the time required to write n nodes is proportional to n. This conclusion makes sense intuitively: It takes longer to display, or traverse, a linked chain of 100 nodes than does a linked chain of 10 nodes.
如果有 n 个节点，这些语句需要 n + 1 次赋值、n + 1 次比较和 n 次写入操作。如果每次赋值、比较和写入操作分别需要 a、c 和 w 个时间单位，则这些语句需要 (n + 1) × (a + c + n × w) 个时间单位。因此，写入 n 个节点所需的时间与 n 成正比。这个结论直观上是合理的：显示或遍历 100 个节点的链表链比显示或遍历 10 个节点的链表链所需时间更长。

> Note: You must traverse a linked chain to access its ith node. The access time is, therefore, directly proportional to i. On the other hand, you can access array items directly, with equal access time for each item.
> 注：你必须遍历链表链才能访问其第 i 个节点。因此，访问时间与 i 成正比。另一方面，你可以直接访问数组项，每个项的访问时间相等。

### The Towers of Hanoi
### 汉诺塔

Chapter 2 proved recursively that the solution to the Towers of Hanoi problem with n disks requires 2^n - 1 moves. If each move requires the same time m, the solution requires (2^n - 1) × m time units. As you will soon see, this time requirement increases rapidly as the number of disks increases.
第 2 章递归证明了 n 个盘子的汉诺塔问题的解需要 2^n - 1 次移动。如果每次移动需要相同的时间 m，则该解需要 (2^n - 1) × m 个时间单位。如你将很快看到，随着盘子数量的增加，此时间需求会迅速增加。

### Nested loops
### 嵌套循环

Consider an algorithm that contains nested loops of the following form:
考虑包含以下形式嵌套循环的算法：

```
for (i = 1 through n)
    for (j = 1 through i)
        for (k = 1 through 5)
            Task J
```

If task $T$ requires $t$ time units, the innermost loop on $k$ requires $5 \times t$ time units. The loop on $j$ requires $5 \times t \times i$ time units, and the outermost loop on $i$ requires
如果任务 T 需要 t 个时间单位，则最内层的 k 循环需要 5 × t 个时间单位。j 循环需要 5 × t × i 个时间单位，而最外层的 i 循环需要
$$
\sum_{i=1}^n (5 \times t \times i) = 5 \times t \times (1 + 2 + \cdots + n) = 5 \times t \times n \times (n + 1)/2
$$
time units.
个时间单位。

### Question 1 How many comparisons of array items do the following loops contain?
### 问题 1 以下循环包含多少次数组项比较？

```cpp
for (j = 1; j <= n-1; j++)
{
    i = j + 1;
    do
    {
        if (theArray[i] < theArray[j])
        swap(theArray[i], theArray[j]);
    } ++i;
    while (i <= n);
} // end for
```

### Question 2 Repeat Question 1, replacing the statement i = j + 1 with i = j.
### 问题 2 重复问题 1，将语句 i = j + 1 替换为 i = j。

### 10.2.2 Algorithm Growth Rates
### 10.2.2 算法增长率

As you can see, the previous examples derive an algorithm's time requirement as a function of the problem size. The way to measure a problem's size depends on the application—typical examples are the number of nodes in a linked chain, the number of disks in the Towers of Hanoi problem, the size of an array, or the number of items in a stack. Thus, we reached conclusions such as
如你所见，前面的示例将算法的时间需求作为问题规模的函数来推导。衡量问题规模的方法取决于应用——典型示例包括链表链中的节点数、汉诺塔问题中的盘子数、数组的大小或栈中的项数。因此，我们得出了诸如以下结论：

### Measure an algorithm's time requirement as a problem size
### 按问题规模衡量算法的时间需求

- Algorithm A requires n^2 / 5 time units to solve a problem of size n
- 算法 A 解决规模为 n 的问题需要 n^2 / 5 个时间单位
- Algorithm B requires 5 × n time units to solve a problem of size n
- 算法 B 解决规模为 n 的问题需要 5 × n 个时间单位

The time units in the previous two statements must be the same before you can compare the efficiency of the two algorithms. If we had written
前两个陈述中的时间单位必须相同，然后才能比较两个算法的效率。如果我们写了

Algorithm A requires n^2 / 5 seconds to solve a problem of size n
算法 A 解决规模为 n 的问题需要 n^2 / 5 秒

our earlier discussion indicates the difficulties with such a statement: On what computer does the algorithm require n^2 / 5 seconds? What implementation of the algorithm requires n^2 / 5 seconds? What data caused the algorithm to require n^2 / 5 seconds?
我们之前的讨论表明这种陈述存在困难：算法在什么计算机上需要 n^2 / 5 秒？算法的哪种实现需要 n^2 / 5 秒？什么数据导致算法需要 n^2 / 5 秒？

What specifically do you want to know about the time requirement of an algorithm? The most important thing to learn is how quickly the algorithm's time requirement grows as a function of the problem size. Statements such as
你具体想了解算法时间需求的什么？最重要的是要了解算法的时间需求作为问题规模的函数增长得有多快。诸如以下陈述

- Algorithm A requires time proportional to n^2
- 算法 A 需要与 n^2 成正比的时间
- Algorithm B requires time proportional to n
- 算法 B 需要与 n 成正比的时间

each express an algorithm's proportional time requirement, or growth rate, and enable you to compare algorithm A with another algorithm B. Although you cannot determine the exact time requirement for either algorithm A or algorithm B from these statements, you can determine that for large problems, B requires significantly less time than A. That is, B's time requirement—as a function of the problem size n—increases at a slower rate than A's time requirement, because n increases at a slower rate than n^2. Even if B actually requires 5 × n seconds and A actually requires n^2 / 5 seconds, B eventually requires significantly less time than A, as n increases. Figure 10-1 illustrates this fact. Thus, a
每个都表达了算法的比例时间需求，即增长率，并使你能够比较算法 A 与另一个算法 B。虽然你无法从这些陈述中确定算法 A 或算法 B 的精确时间需求，但你可以确定对于大型问题，B 所需的时间比 A 显著少。也就是说，B 的时间需求——作为问题规模 n 的函数——以比 A 的时间需求更慢的速率增加，因为 n 的增长速率比 n^2 慢。即使 B 实际上需要 5 × n 秒而 A 实际上需要 n^2 / 5 秒，随着 n 的增加，B 最终也将比 A 少花费显著更少的时间。图 10-1 说明了这一事实。因此，一个

### Compare algorithm efficiencies for large problems
### 比较大型问题的算法效率

