

该和的类型的类型与 'T' 类的 "getValue" 函数返回的类型相同。此时，该类型仍未指定。因此，它用模板符号 'S' 表示，由实际调用该函数的用户稍后指定。

在我们的应用中，'S' 始终为 "double"；在更高级的应用中，它也可以代表复数。

符号 'S' 的具体解释取决于作为引用传递给函数的参数 "compare"。该参数用于确定当前链表中哪些项太小应从中删除：

```cpp
template<class T>
template<class S>
const S linkedList<T>::truncateItems(double threshold,
    const S& compare) {
    S sum = 0.;
    if (next) {
        int dropped = 0;
```

下面的循环使用指向链表的指针 "runner" 从当前链表中的一项推进到下一项。在循环中，并非由 "runner" 指向的项，而是其后面的项由 "dropNextItem" 函数考虑是否删除。如果该项确实应被删除，则局部整数变量 "dropped" 取值为 1，这意味着 "runner" 已推进到下一项。反之，如果该项不应被删除，则 "dropped" 取值为 0，这意味着应手动将 "runner" 推进到下一项以继续循环：

```cpp
for (linkedList<T>* runner = this;
    runner->next;
    runner = dropped ? runner : runner->next) {
    dropped = 0;
    if (fabs(runner->next->item.getValue())
        <= threshold * fabs(compare)) {
        sum += runner->next->item.getValue();
        runner->dropNextItem();
        dropped = 1;
    }
}
```

最后，当前链表中的第一项也应考虑是否删除：

```cpp
if (next && (fabs(item.getValue())
    <= threshold * fabs(compare))) {
    sum += item.getValue();
    dropFirstItem();
}
return sum;
} // truncate small items
```

以下是另外两个与上述函数非常相似的函数。事实上，它们与之的区别仅在于删除项的标准。它们假定 'T' 类还具有 "getColumn" 函数，该函数返回一个整数，用以表征该项在链表中的位置。事实上，由 "getColumn" 函数返回的整数可视为链表中该项的（可能不连续的）索引：链表中的第一项具有最小索引，下一个项具有（可能大得多）的更大索引，依此类推，直到链表中的最后一项，它具有最大索引。

下面的 "dropPositiveItems" 函数接收两个额外参数：整数 "diag" 和 'S' 对象 "center"。删除项的标准是其由 "getColumn" 函数返回的索引是否不同于 "diag"，以及其大小是否很小或其符号与 "center" 相同：

```cpp
template<class T>
template<class S>
const S linkedList<T>::dropPositiveItems(
    int diag, const S& center, double threshold) {
    S sum = 0.;
    if (next) {
        int dropped = 0;
        for (linkedList<T>* runner = this;
            runner->next;
            runner = dropped ? runner : runner->next) {
            dropped = 0;
            if ((double(runner->next->item.getValue() / center)
                >= -threshold) &&
                (runner->next->item.getColumn() != diag)) {
                sum += runner->next->item.getValue();
                runner->dropNextItem();
                dropped = 1;
            }
        }
    }
    if (next && (double(item.getValue() / center) >= -threshold)
        && (item.getColumn() != diag)) {
        sum += item.getValue();
        dropFirstItem();
    }
    return sum;
} // drop positive or small items
```

另一个与上述函数非常相似的函数是 "maskItems" 函数。在该函数中，链表中的项由作为引用传递给它的整数向量 "masked"。这样，只有其 "getColumn()" 索引对应于该向量中非零分量的项保留在当前链表中，而所有其他项都从中删除。

传递给函数的第二个参数在代码中实际上从未使用。它的唯一目的是在用户实际调用函数时指定类型 'S'。该类型随后用于定义局部变量 "sum"，它包含被删除项的和：

```cpp
template<class T>
template<class S>
const S linkedList<T>::maskItems(
    const dynamicVector<int>& mask, const S&) {
    S sum = 0.;
    if (next) {
        int dropped = 0;
        for (linkedList<T>* runner = this;
            runner->next;
            runner = dropped ? runner : runner->next) {
            if (!mask[runner->next->item.getColumn()]) {
                sum += runner->next->item.getValue();
                runner->dropNextItem();
                dropped = 1;
            }
        }
    }
    if (next && (!mask[item.getColumn()])) {
        sum += item.getValue();
        dropFirstItem();
    }
    return sum;
} // masking items
```

## 3.8 合并问题

链表的用户可能希望以多种方式操作它们。例如，他们可能希望向其中插入项或从中删除项。此外，他们希望能够在无需处理指针和地址等存储问题的情况下完成此操作。执行这些任务的函数如上所述。

链表的用户可能还希望执行另一种操作：将两个有序链表合并在一起，同时保持顺序。高效完成此任务称为合并问题。

模板的强大之处在此显现。事实上，处理未指定的类型 'T' 特别方便，前提是它支持某种顺序。这样，我们就可以专注于所考虑的数据结构，而非其中变量所使用的类型。只有在调用合并函数时，具体类型才会被指定。

下面，我们描述一个将两个链表合并为单个链表同时保持顺序的函数。假定链表中项的类型 'T' 支持完整的优先级顺序；也就是说，每两个 'T' 对象都可以通过 '<'、'>' 和 "==" 二元运算符进行比较。

该优先级顺序可能有各种不同的解释。事实上，如果 'T' 类的 '<'、'>' 和 "==" 运算符具有通常含义，则 'T' 类中的项应按递增值的顺序排列，从最小到最大。反之，如果这些运算符在 'T' 类中按绝对值解释，则链表中的项应按递增幅度的顺序排列，从幅度最小到幅度最大（参见第 3.22 节的练习）。

然而，在本书后面使用的应用中，并未使用这两种解释。事实上，上述优先级顺序是根据 `T` 类中可用的 "getColumn()" 函数诱导的：一个 `T` 对象并非因其（绝对）值小于另一个而优先于（“小于”）另一个，而是因其 "getColumn()" 索引小于另一个。

还假定当前的 `linkedList` 对象和合并到其中的 `linkedList` 参数在意义上是良好有序的，即每一项都优先于（“小于”）下一项。

目的是将作为参数传递的链表合并到当前链表中，同时保持正确的优先级顺序。此操作在第 16 章实现的稀疏矩阵中特别有用。

还假定 `T` 类支持 "+=" 运算符。在这些假设下，使用 "+=" 运算符将链表合并到当前链表中也可以定义。

![](img/1f293b0ceb2de964310ea7f941a1b580_145_0.png)

**图 3.3.** *合并两个链表同时保持顺序。* 顶部链表（当前对象）中的项由外层循环中的指针 "runner" 扫描。底部链表 `L`（参数）中的项由内层循环中的指针 "Lrunner" 扫描并插入到正确位置。

代码使用两个“runner”扫描链表中的项（见图 3.3）。主 runner 扫描当前链表中的项。由该 runner 指向的项与其后项之间的空间应由作为参数传递的第二个链表中的项填充，前提是它们确实按顺序属于那里。为此，使用一个称为 "Lrunner" 的次要 runner 来扫描确实属于主 runner 所指向位置的第二个链表中的项。这些项随后逐一按其正确位置插入到当前链表中。

如果第二个链表中的一项与当前链表中现有项具有相同的优先级顺序 `<`，即在 `T` 类的 `"=="` 运算符意义上相等，则它使用 `T` 类的 `"+="` 运算符加到该项上。这种方法确实。

