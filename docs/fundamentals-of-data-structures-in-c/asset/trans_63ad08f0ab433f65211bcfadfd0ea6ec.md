

```c
poly *insertNode(poly *head, poly *p)
{
    if(p -> coef == 0.0F)
        return head;
    if(head == NULL)
        return p;
    else if(p -> exp > head -> exp)
    {
        p -> next = head;
        return p;
    }
    else if(p -> exp < head -> exp)
        head -> next = insertNode(head -> next, p);
    else if(p -> exp == head -> exp)
    {
        head -> coef = head -> coef + p -> coef;
        if(head -> coef == 0.0F)
            return head -> next;
    }
    return head;
}

void viewPoly(poly * ply)
{
    if(ply == NULL)
        printf("NULL\n");
    while(ply != NULL)
    {
        printf("%.2fx^%d", ply -> coef, ply -> exp);
        printf("%s", (ply -> next == NULL) ? " = 0\n" : " + ");
        ply = ply -> next;
    }
}

poly * polyAdd(poly *poly1, poly *poly2)
{
    poly *head = NULL;
    while(poly1 != NULL)
    {
        head = insertNode(head, copyNode(poly1, POSITIVE));
        poly1 = poly1 -> next;
    }
    while(poly2 != NULL)
    {
        head = insertNode(head, copyNode(poly2, POSITIVE));
        poly2 = poly2 -> next;
    }
    return head;
}
poly * polySub(poly *poly1, poly *poly2)
{
    poly *head = NULL;
    while(poly1 != NULL)
    {
        head = insertNode(head, copyNode(poly1, POSITIVE));
        poly1 = poly1 -> next;
    }
    while(poly2 != NULL)
    {
        head = insertNode(head, copyNode(poly2, NEGATIVE));
        poly2 = poly2 -> next;
    }
    return head;
}
poly * polyMul(poly *poly1, poly *poly2)
{
    if(poly2 == NULL)
        return NULL;
    else
        return polyAdd(mulNode(poly1,poly2),polyMul(poly1,poly2->next));
}
poly * copyNode(poly * p, int sign)
{
    poly *newnode;
    newnode = getNode();
    newnode -> coef = sign * p -> coef;
    newnode -> exp = p -> exp;
    newnode -> next = NULL;
    return newnode;
}

poly *mulNode(poly *p1, poly *p2)
{
    poly *temp = NULL;
    if(p1 != NULL)
    {
        temp = getNode();
        temp -> coef = p1 -> coef * p2 -> coef;
        temp -> exp = p1 -> exp + p2 -> exp;
        temp -> next = mulNode(p1->next, p2);
    }
    return temp;
}

/* For Quotient and Remainder p1 / p2 */

poly *polyDiv(poly *p1, poly *p2, poly **rmdr)
{
    poly *res = NULL;
    if(p1 == NULL || p2 == NULL)
        return (*rmdr = NULL);
    if(p1 -> exp >= p2 -> exp)
    {
        res = getNode();
        res -> coef = p1 -> coef / p2 -> coef;
        res -> exp = p1 -> exp - p2 -> exp;
        res -> next = polyDiv(polySub(p1,mulNode(p2,res)),p2,rmdr);
    }
    else
        *rmdr = p1;
    return res;
}
```

## 程序显示以下输出

- 使用单链表的多项式操作 ...
- 0. 查看主菜单
- 1. 创建第一个多项式
- 2. 创建第二个多项式
- 3. 查看第一个和第二个多项式
- 4. 多项式加法
- 5. 多项式减法
- 6. 多项式乘法
- 7. 多项式除法
- 8. 退出

? 3
第一个多项式是 ...
NULL
第二个多项式是 ...
NULL
? 4
加法后的结果多项式是 ...
NULL
? 5
减法后的结果多项式是 ...
NULL
? 6
乘法后的结果多项式是 ...
NULL
? 7
除法后的结果多项式是 ...
解是无穷大 ...
解是无穷大 ...
商：NULL
余数：NULL
? 1
请输入第一个多项式 . . .
请输入系数：3
请输入指数：2
请输入系数：2
请输入指数：1
请输入系数：1
请输入指数：0
第一个多项式为：3.00x^2 + 2.00x^1 + 1.00x^0 = 0
? 2
请输入第二个多项式 . . .
请输入系数：2
请输入指数：1
请输入系数：3
请输入指数：1
请输入系数：5
请输入指数：0
第二个多项式为：5.00x^1 + 5.00x^0 = 0

? 3
第一个多项式是 ...
3.00x^2 + 2.00x^1 + 1.00x^0 = 0
第二个多项式是 ...
5.00x^1 + 5.00x^0 = 0
? 4
加法后的结果多项式是 ...
3.00x^2 + 7.00x^1 + 6.00x^0 = 0
? 5
减法后的结果多项式是 ...
3.00x^2 + -3.00x^1 + -4.00x^0 = 0
? 6
乘法后的结果多项式是 ...
15.00x^3 + 25.00x^2 + 15.00x^1 + 5.00x^0 = 0
? 7
除法后的结果多项式是 ...
商：0.60x^1 + -0.20x^0 = 0
余数：2.00x^0 = 0
? 8
您的程序运行结束 . . .

程序 3.8 能够以任意顺序读取输入，同时也能读取指数值为零的输入。如果您反复输入相同的指数值，它将自动将相同指数的系数相加，并按降序存储。您还可以修改任意一个现有多项式，并用旧多项式对新多项式进行操作（加、减、乘、除）。

## 链表的优点

- 在声明链表时无需指定元素数量（因为在向列表添加节点时可以动态分配内存）。
- 链表的大小可以根据列表中的插入和删除操作而增长和缩小。
- 列表中任何位置的插入和删除都可以轻松高效地处理。
- 链表不会浪费任何内存空间。

## 链表的缺点

- 在列表中查找特定元素既困难又耗时。
- 链表存储相同数量的元素所需的存储空间比数组多（. . . 列表中的每个元素都需要额外的内存空间来存储下一个节点的地址）。

## 3.10 总结

- 链表的一些重要应用是栈和队列。
- 栈可以通过数组或链表实现。
- 栈是有序元素集合，插入和删除操作仅限于一端。元素添加和/或移除的端称为栈顶。
- 栈被称为后进先出（LIFO）列表、堆栈或压栈列表。
- 栈可以执行的基本操作是 push、pop 和 peek 操作。
- push 是用于向栈中添加新元素的操作。
- pop 是用于从栈中移除最顶部元素的操作。
- peek 是用于显示栈中最顶部元素的操作。
- 在栈的数组表示中，如果栈不包含任何元素，则称为空栈。
- 在栈的数组表示中，如果栈包含的元素数量等于其大小，则称为已完全占用的栈。
- 在链表中，如果栈指向 NULL，则该栈被称为空栈。
- 如果链表中 malloc 函数返回 NULL，则称为已完全占用的栈。
- 栈的一些重要应用包括汉诺塔、字符串反转、检查括号匹配以及算术表达式求值。
- 汉诺塔是一个游戏，我们得到一个由 n 个磁盘组成的塔，最初从上到下按尺寸递增堆叠。在这个塔旁边，还有两个塔。目标是使用塔 2 将所有磁盘从塔 1 移动到塔 3。
- 给定一个算术表达式，我们所说的“平衡”确切意思是，各种形状的左括号（圆括号、方括号或花括号）必须与同一形状的对应最后未匹配的右括号符号匹配，并且当算术表达式结束时，所有括号符号都必须匹配。
- 表示算术表达式的不同记数法包括中缀记法、前缀记法和后缀记法。
- 表示数学表达式的常规方式称为中缀记法。
- 前缀记法（也称为波兰记法）是一种编写代数表达式的方式，不使用括号或运算符优先级规则。

后缀记法（也称为后缀形式或逆波兰记法（RPN））也是一种编写代数表达式的方式，不使用括号或运算符优先级规则。

队列是有序元素集合，插入操作在一端进行，删除操作在另一端进行。进行插入的端称为队尾，进行删除的端称为队首。

队列可以执行的基本操作是入队和出队操作。

入队是用于向队列队尾添加新元素的操作。

出队是用于从队列队首移除元素的操作。

循环队列是线性队列的另一种形式，其中最后一个节点连接到列表的第一个节点。

双端队列（Deque）是队列的另一种形式，插入和删除操作在队列的队首和队尾都进行。

双端队列有两种变体，即输入受限双端队列和输出受限双端队列。输入受限双端队列仅允许在一端（可以是队首或队尾）进行插入。输出受限双端队列仅允许在一端（可以是队首或队尾）进行删除。

循环队列的实现部分与线性队列相同，只是最后一个位置连接到队列的第一个位置。因此，队首和队尾循环移动。

循环双端队列的实现部分与线性双端队列相同，只是最后一个位置连接到双端队列的第一个位置。因此，队首和队尾循环移动。

## 3.11 简答题

- 1. 定义栈。

栈是有序元素集合，插入和删除操作仅限于一端。元素添加和/或移除的端称为栈顶。栈也称为“堆栈”和“压栈列表”。

- 2. 列出可以在栈和队列上执行的基本操作。

栈和队列可以执行的基本操作如下，

- push 操作
- pop 操作
- 查看栈内容。

