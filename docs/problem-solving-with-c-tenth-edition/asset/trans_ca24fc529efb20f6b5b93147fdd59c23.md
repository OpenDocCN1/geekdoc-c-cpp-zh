

## DISPLAY 18.2 双向和随机访问迭代器使用（第 2 部分，共 2 部分）

```
25     cout << "Two steps forward and one step back:\n";
26     p++;
27     cout << *p << endl;
28     p++;
29     cout << *p << endl;
30     p--;
31     cout << *p << endl;
32     return 0;
33 }
```

这是递减运算符。它适用于任何双向迭代器。

## Sample Dialogue

```
container[0] == A
container[1] == B
container[2] == C
container[3] == D
The third entry is C
The third entry is C
The third entry is C
Back to container[0].
which has value A
Two steps forward and one step back:
B
C
B
```

递减运算符在 Display 18.2 中使用，其中包含它的行以高亮显示。正如你所期望的，p-- 将迭代器 p 移动到前一个位置。递减运算符 -- 与递增运算符 ++ 相同，但它使迭代器朝相反方向移动。

递增和递减运算符都可以用前缀（++p）或后缀（p++）记法使用。除了改变 p，它们还返回一个值。返回值的细节与对 int 变量使用递增和递减运算符时的情况完全类似。在前缀记法中，首先改变变量并返回改变后的值。在后缀记法中，先返回值再改变变量。我们更倾向于不将递增和递减运算符用作返回值的表达式，而只用它们来改变变量值。

Display 18.2 中的以下行说明了使用 vector 迭代器时，你可以随机访问 vector 的元素，例如 container：

```
vector<char>::iterator p = container.begin();
cout << "The third entry is " << container[2] << endl;
cout << "The third entry is " << p[2] << endl;
cout << "The third entry is " << *(p + 2) << endl;
```

随机访问意味着你可以在一步内直接到达任何特定元素。我们已经使用 container[2] 作为对 vector 的随机访问形式。它只是数组和 vector 标准使用的方括号运算符。新的地方在于你可以用这种相同的方括号记法来使用迭代器。表达式 p[2] 是一种获得索引为 2 的元素访问的方式。

表达式 p[2] 和 *(p + 2) 完全等价。通过类比指针算术（参见第 9 章），(p + 2) 命名了 p 之外的两个位置。由于 p 在上述代码中位于第一个（索引 0）位置，(p + 2) 位于第三个（索引 2）位置。表达式 (p + 2) 返回一个迭代器。表达式 *(p + 2) 对该迭代器进行解引用。当然，你可以用不同的非负整数替换 2 来获得指向不同元素的指针。

请注意，p[2] 也不改变迭代器变量 p 中的迭代器值。表达式 (p + 2) 返回另一个位置的另一个迭代器，但它让 p 保持原位。p[2] 也是如此。还请注意，p[2] 和 (p + 2) 的含义取决于 p 中迭代器的位置。例如，(p + 2) 表示 p 所在位置之外的两个位置，无论它在哪里。

例如，假设 Display 18.2 中之前讨论的代码被以下内容替换（注意添加了 p++）：

```
vector<char>::iterator p = container.begin();
p++;
cout << "The third entry is " << container[2] << endl;
cout << "The third entry is " << p[2] << endl;
cout << "The third entry is " << *(p + 2) << endl;
```

这三个 cout 的输出将不再是

```
The third entry is C
The third entry is C
The third entry is C
```

而将是

```
The third entry is C
The third entry is D
The third entry is D
```

p++ 将 p 从位置 0 移动到位置 1，因此 (p + 2) 现在是一个位于位置 3 而不是位置 2 的迭代器。因此，*(p + 2) 和 p[2] 等价于 container[3]，而不是 container[2]。

## Kinds of Iterators

不同的容器具有不同种类的迭代器。以下是主要迭代器种类：

**Forward iterators:** ++ 在迭代器上工作。

**Bidirectional iterators:** ++ 和 -- 都在迭代器上工作。

**Random access iterators:** ++、-- 和随机访问都与迭代器一起工作。

我们现在对迭代器了解足够多，可以理解迭代器是如何分类的。迭代器的主要种类是

**Forward iterators:** ++ 在迭代器上工作。

**Bidirectional iterators:** ++ 和 -- 都在迭代器上工作。

**Random access iterators:** ++、-- 和随机访问都与迭代器一起工作。

请注意，这些是越来越强的类别：每个随机访问迭代器也是一个双向迭代器，每个双向迭代器也是一个前向迭代器。正如我们将看到的，不同的模板容器类具有不同种类的迭代器。vector 模板类的迭代器是随机访问迭代器。

请注意，名称 *forward iterator*、*bidirectional iterator* 和 *random access iterator* 指的是迭代器的种类，而不是类型名。实际的类型名将是类似 `std::vector<int>::iterator` 的东西，在这种情况下它恰好是一个随机访问迭代器。

## SELF-TEST EXERCISE

4. 假设 vector v 按顺序包含字母 'A'、'B'、'C' 和 'D'。以下代码的输出是什么？

```
vector<char>::iterator i = v.begin();
i++;
cout << *(i + 2) << " ";
i--;
cout << i[2] << " ";
cout << *(i + 2) << " ";
```

## Constant and Mutable Iterators

类别 forward iterator、bidirectional iterator 和 random access iterator 各自又细分为两个类别：constant 和 mutable，这取决于解引用运算符与迭代器的行为方式。使用 constant 迭代器时，解引用运算符产生元素的只读版本。使用 constant 迭代器 p 时，你可以使用 *p 例如将其赋给变量或输出到屏幕，但你不能通过例如将 *p 赋值为某个值来改变容器中的元素。使用 mutable 迭代器 p，*p 可以赋一个值，这将改变容器中对应的元素。vector 迭代器是 mutable 的，如 Display 18.1 中的以下行所示：

```
cout << "Setting entries to 0:\n";
for (p = container.begin(); p != container.end(); p++)
    *p = 0;
```

如果一个容器只有 constant 迭代器，你就无法为该容器获得 mutable 迭代器。然而，如果一个容器具有 mutable 迭代器并且你想要为该容器获得一个 constant 迭代器，你可以拥有它。你可能想要一个 constant 迭代器作为一种错误检查，如果你打算让你的代码不改变容器中的元素。例如，以下内容将为名为 container 的 vector 容器生成一个 constant 迭代器：

```
std::vector<char>::const_iterator p = container.begin();
```

或等价地

```
using std::vector<char>::const_iterator;
const_iterator p = container.begin();
```

以这种方式声明 p 后，以下内容将产生错误信息：

```
*p = 'Z';
```

例如，Display 18.2 将完全相同地运行，如果你将

```
vector<int>::iterator p;
```

改为

```
vector<int>::const_iterator p;
```

然而，类似的更改在 Display 18.1 中将不起作用，因为 Display 18.1 程序中的以下行：

```
*p = 0;
```

请注意 const_iterator 是一个类型名，而 constant iterator 是迭代器的一种种类的名称。然而，每一个类型名为 const_iterator 的迭代器都将是一个 constant 迭代器。

## Constant Iterator

Constant iterator 是一个不允许你改变其所在位置元素的迭代器。

## Reverse Iterators

有时你想以相反顺序遍历容器中的元素。如果有一个具有双向迭代器的容器，你可能会想尝试

```
vector<int>::iterator p;
for (p = container.end(); p != container.begin(); p--)
    cout << *p << " ";
```

这段代码会编译，并且你可能能在某些系统上让它工作，但这里有一个根本性的错误：container.end() 不是一个常规迭代器，而只是一个哨兵，而 container.begin() 不是一个哨兵。

幸运的是，有一个简单的方法来实现你想要的功能。对于具有双向迭代器的容器，有一种方法可以使用一种称为 reverse iterator 的迭代器来反转一切。以下内容将正常工作：

```
vector<int>::reverse_iterator rp;
for (rp = container.rbegin(); rp != container.rend(); rp++)
    cout << *rp << " ";
```

成员函数 rbegin() 返回位于最后一个元素的迭代器。成员函数 rend() 返回一个哨兵，标记元素在反向顺序中的“末尾”。请注意，对于类型为 reverse_iterator 的迭代器，递增运算符 ++ 通过元素向后移动。换句话说，-- 和 ++ 的含义被互换了。Display 18.3 中的程序演示了 reverse iterator。

## Reverse Iterators

Reverse iterator 可用于遍历容器的所有元素，前提是容器具有双向迭代器。
一般方案如下：

```
STL_Container<type>::reverse_iterator rp;
for (rp = c.rbegin(); rp != c.rend(); rp++)
    Process_At_Location rp;
```

对象 c 是一个具有双向迭代器的容器类。

