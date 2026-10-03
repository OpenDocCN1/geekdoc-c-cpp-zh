
# 第 17 章 动态向量与列表

## 17.8 赋值运算符

下面定义的赋值运算符也使用了链表的递归结构：首先，赋值链表的尾部。

```cpp
template<class T>
const linkedList& linkedList::operator=(const linkedList&l) {
```

如果用户尝试赋值 `l`，则什么都不需要做。另一方面，如果赋值是非平凡的，则进入以下 `if` 块：

```cpp
if(this != &l){
```

首先，当前链表的第一个项被赋值为与 `l` 相同：

```cpp
item = l.item();
```

接下来，递归地赋值链表的尾部。为了这一点，有两种情况：如果当前列表有尾部，

```cpp
if(next){
```

```cpp
if(l.next)
    *next = *l.next;
else
    delete next;
next = 0;
}
```

另一方面，如果当前列表没有尾部，则使用拷贝构造函数附加 `l` 的尾部：

```cpp
else
if(l.next)next = new linkedList(*l.next);
}
```

最后，返回链表的常量引用：

```cpp
return *this;
} // 赋值运算符
```

这样用户就可以编写 `l3 = l2 = l1` 将链表 `l1` 赋值给 `l2` 和 `l3`。

## 17.9 删除项

与普通列表不同，链表可以轻松高效地删除项。例如，这里是删除链表中第二个项的函数：

```cpp
template<class T>
void linkedList<T>::dropNextItem(){
```

首先，我们必须询问确实有一个第二个项可以删除：

```cpp
if(next){
```

现在，有两种可能的情况：如果链表中还有第三项，

```cpp
if(next->next){
```

那么我们必须确保在移除指向它的第二个项时它不会丢失。为了这个目的，我们将链表尾部的地址保留在本地指针 `keep` 中：

```cpp
linkedList<T>* keep = next;
```

这样，我们可以将原始尾部替换为不再包含原始链表中第二个项的短尾部：

```cpp
next = next->next;
```

然而，被删除的项仍然占用内存。幸运的是，我们仔细地通过本地指针 `keep` 跟踪了它。现在可以使用该指针通过 `T` 类的析构函数完全销毁它：

```cpp
keep->item();
```

这样，`next` 指向原始链表中的第三项而不是第二个，符合要求。

如果原始链表中没有第三项，则删除整个尾部（包含第二个项）：

```cpp
else{
    delete next;
    next = 0;
}
```

如果链表中没有第二个项可以删除，则在屏幕上打印错误信息：

```cpp
else
printf("error: cannot drop nonexistent next item\n");
} // 移除链表中的第二个项
```

这完成了删除链表中第二个项的函数编写。实际上，该函数也可以通过将其应用到由 `next` 指向的当前链表的末尾，来删除第三个项，依此类推。

此外，上述函数在删除链表中的第一个项时也是很有用的：

```cpp
template<class T>
void linkedList<T>::dropFirstItem(){
```

事实上，如果当前链表中存在第二个项，

```cpp
if(next){
```

那么它的一个重复副本也会存储在第一个项中：

```cpp
item = next->item;
```

然后，调用 `dropNextItem` 函数来按需要删除第二个重复副本：

```cpp
dropNextItem();
}
```

另一方面，如果原始列表中没有第二个项，则无法删除第一个项，否则列表将保持完全为空。因此，应该打印一条错误信息：

```cpp
else
printf("error: cannot drop the only item.\n");
} // 移除链表中的第一个项
```

所以我们看到，链表对象必须包含一个项；任何尝试删除此项的尝试都会导致错误。因此，用户必须小心不要这样做。虽然这并不理想，但这种实现对于我们书中的应用已经足够了。然而，在下面，我们还介绍了栈对象，它对链表进行了改进，并在必要时可以完全清空。

链表的递归结构也有助于将其打印到屏幕上。事实上，在打印了第一个项后，`print` 函数被递归地应用到末尾，以打印链表中的其余项：

```cpp
template<class T>
void print(const linkedList<T>&l){
printf("item:\n");
```

```cpp
print(1());
if(1.readNext())print(*1.readNext());
} // 递归地打印链表
```

这里有一个显示链表在实践中使用的示例：

```cpp
int main() {
  linkedList<double> c(3);
  c.append(5.);
  c.append(6);
  c.dropFirst();
  print(c);
  return 0;
}
```

这段代码产生了一个类型为 `double` 的项的链表，其中包含项 3、5 和 6。（因为 3 < 5 < 6，这样的列表被称为有序列表。）然后，列表中的第一个项被删除。最后，剩余的项 5 和 6 被打印到屏幕上。

## 17.10 合并问题

假设用于链表中的类 `T` 有一个定义良好的 `operator<`，以便对类型为 `T` 的对象施加完全顺序。例如，如果 `T` 被解释为整数类型，那么 `<` 可能具有通常含义：`m < n` 意味着 `m` 小于 `n`。有序列表是指保持这种顺序的列表，从意义上说，较小的项（根据类 `T` 中的 `<` 运算符）必须出现在列表中一个比它大的项之前。例如，5, 3, 6 就不是。

在合并过程中，两个列表应该高效地合并成一个有序列表。正如我们将在下面看到的，得益于可以轻松引入新项和丢弃旧项，链对象适用于这一目的。

在接下来，假设类型 `T` 对象可以通过 `<`、`>` 或 `+=` 二进制运算符进行比较。还假设当前的 `linkedList` 对象和要合并进的参数都是有序的，即每个项都小于下一个项。

还假设 `T` 类支持 `+` 运算符。这样，如果在合并过程中遇到两个相等的项，就可以简单地将它们相加，形成一个包含它们之和的新项。该运算符用在下面 `linkedList` 类中定义的 `+=` 运算符中，该运算符将参数列表合并到当前链表中。

![图 17.3：将两个有序链表合并为一个有序链表。上方链表（当前对象）中的项由外部循环中的指针 `runner` 扫描。下方链表 `L`（参数）中的项由内部循环中的指针 `Lrunner` 扫描，并插入到正确的位置。](img/57402a72d6abfaa2dd5e70d5e16a53ab_392_0.png)

使用两个指针扫描链表中的项以实现合并的代码（见图 17.3）。命名为 `runner` 的主指针扫描当前链表中的项。`runner` 指向的项与下一个项之间的空间应该由作为参数传递给函数的第二个链表中的项填充。为了这个目的，使用一个名为 `Lrunner` 的辅助指针来扫描第二个链表，并找到在顺序上确实属于那里的项。这些项随后被一个一个插入此列表。

如果第二个链表中的项与当前链表中的现有项具有相同的优先级顺序 `<`

```cpp
template<class T>
const linkedList<T>&operator+=(linkedList<T>&L) {
  linkedList<T>* runner = this;
  linkedList<T>* Lrunner = &L;
```

这里，`runner` 指针在 `Lrunner` 指针循环之前已经定义。`runner` 指向当前链表。此外，`Lrunner` 指向作为参数传递的链表 `L`。为了开始合并过程，我们需要 `L` 中的链表项小于当前链表项。在这种情况下，`Lrunner` 指向 `L` 链表的第一个项。

```cpp
if(Lrunner->item < item) {
    insertFirst(Lrunner->item);
    Lrunner = Lrunner->next;
}
```

我们现在准备好开始合并过程。此时，`runner` 指向的项与下一个项之间的空间应该由作为参数传递给函数的第二个链表中的项填充。为了这个目的，使用一个名为 `Lrunner` 的辅助指针来扫描第二个链表，并找到在顺序上确实属于那里的项。

```cpp
while(runner->next) {
  while(Lrunner && Lrunner->item < runner->next) {
    insertNext(Lrunner->item);
    Lrunner = Lrunner->next;
  }
  runner = runner->next;
}
```

这结束了外部循环。仍然，`L` 可能包含大于或等于当前链表项的项。

```cpp
while(Lrunner) {
  if(Lrunner->item == runner->item) {
    runner->item += Lrunner->item;
    Lrunner = Lrunner->next;
  } else {
    insertNext(Lrunner->item);
    runner = runner->next;
    Lrunner = Lrunner->next;
  }
}
```

上面的逻辑有些碎片化。让我们提供合并逻辑的清晰实现：

```cpp
template<class T>
const linkedList<T>&operator+=(linkedList<T>&L) {
  linkedList<T>* runner = this;
  linkedList<T>* Lrunner = &L;

  if(Lrunner->item < item) {
    insertFirst(Lrunner->item);
    Lrunner = Lrunner->next;
  }

  while(runner->next) {
    while(Lrunner && Lrunner->item < runner->next) {
      insertNext(Lrunner->item);
      Lrunner = Lrunner->next;
    }
    runner = runner->next;
  }

  while(Lrunner) {
    if(Lrunner->item == runner->item) {
      runner->item += Lrunner->item;
      Lrunner = Lrunner->next;
    } else {
      insertNext(Lrunner->item);
      runner = runner->next;
      Lrunner = Lrunner->next;
    }
  }

  return *this;
} // 保持顺序合并两个链表
```

## 17.11 排序问题

假设给定一个无序列表。排序问题是为了根据优先级顺序 `<` 重新排列项，使得给定的项小于下一个项。显然，这必须尽可能高效地完成。

仍然，有一个高效算法来正确排序列表是不够的。事实上，该算法还必须在计算机上高效地实现。为了这个目的，链表是最合适的。

递归排序算法如下（见图 17.4）。首先，将原始列表分为两个子列表。然后，递归使用排序算法将这些子列表处于正确的顺序。最后，合并子列表。

![图 17.4: 排序算法：将原始列表拆分为两个子列表，首先通过递归调用进行正确排序，然后合并成一个有序良好的列表。](img/57402a72d6abfaa2dd5e70d5e16a53ab_395_0.png)

合并成一个有序良好的列表。为了实现这一点，上面定义的 `+=` 运算符最为有用。

该递归在下方的 `order()` 成员函数中实现。传递函数的整数参数 `length` 表示当前链表中的项目数量。这就是为什么 `order()` 函数被递归地应用于它应该处理的子列表，并对它们传递较小的参数 `length/2` 或左右的值。

```cpp
template<class T>
linkedList<T>&
linkedList<T>::order(int length){
```

如果列表只包含一个项目，那么它已经是有序的，因此什么都不需要做。相反，如果它包含多个项目，则应该将其拆分为两个子列表。显然，第一个子列表由 `this` 指向，即当前链表的地址。然而，找到第二个子列表的地址则更为复杂。为了做到这一点，我们定义了局部指针 `runner`，将其初始化为 `this`，然后逐个项目移动，直到到达原始列表的中间：

```cpp
if(length>1){
linkedList<T>* runner = this;
for(int i=0; i<length/2-1; i++)
runner = runner->next;
```

当循环结束时，`runner` 指向第一个子循环中的最后一个项目。因此，可以使用它来定义局部指针 `second`，该指针指向第二个子列表：

```cpp
linkedList<T>* second = runner->next;
```

此外，`runner` 还可以用于从原始列表中移除第二个子列表，使得 `this` 仅指向第一个子列表，而不是整个列表：

```cpp
runner->next = 0;
```

我们现在准备好进行递归了。事实上，当前的 `order()` 函数被递归应用于 `this` 指向的第一个子列表：

```cpp
order(length/2);
```

此外，得益于（如下文所示）`order()` 函数还会返回有序良好列表的引用，第二个子列表可以递归地排序并合并到第一个子列表（由 `this` 指向）中，形成一个所需的有序良好的列表：

```cpp
*this += second->order(length-length/2);
}
```

最后，该函数返回当前链表在最终顺序下的引用：

```cpp
return *this;
} // 对一个无序的链表进行排序
```

## 17.12 栈

在第 1 章第 1.8 节中讨论的栈对象现在可以派自 `LinkedList` 类。这确实为栈对象提供了所需的属性：在项目数量上具有无限容量，并且能够逐个向其顶部推入新项目，并逐个从从中弹出项目。

显然，为了从栈中弹出项目，必须首先检查栈是否为空。为了这一目的，`stack` 类应该包含一个基类 `LinkedList` 类未包含的额外字段。该整数字段命名为 `empty`，当栈为空时取值为 1，否则为 0。

得益于 `item` 和 `next` 字段在基类 `LinkedList` 类中被声明为 `protected`（而不是 `private`），它们也可以从派生的 `stack` 类中访问。这种派生方式如下：

```cpp
template<class T>
class stack : public LinkedList<T>{
  int empty;

public:
    stack():empty(1){
        // 默认构造函数
```

此默认构造函数使用初始化列表将字段 `empty` 设置为 1，表示构造了一个空栈。此外，它隐式地调用了基类 `linkedList` 类的默认构造函数，该函数会将 `next` 字段初始化为零值，以表示这是一个平凡的栈。接下来，我们实现另一个公共成员函数，可用于验证栈是否为空：

```cpp
int isEmpty() const{
    return empty;
} // 检查栈是否为空
```

接下来，我们实现将项目推入栈部的成员函数。如果栈为空，则只需通过将继承自 `LinkedList` 类的 `item` 字段设置为所需的值来实现：

```cpp
void push(const T& t){
    if(empty){
        item = t;
        empty = 0;
    }
```

相反，如果栈不为空，人们自然想要使用继承自 `LinkedList` 类的 `insertBefore` 函数：

```cpp
    else{
        insertBefore(t);
    } // 将项目推入栈顶
```

接下来，我们实现从栈中弹出项目的成员函数。当然，如果栈为空，必须在屏幕上打印错误消息：
