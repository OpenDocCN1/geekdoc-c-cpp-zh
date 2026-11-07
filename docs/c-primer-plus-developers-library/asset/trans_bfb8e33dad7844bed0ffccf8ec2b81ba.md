
假设我们随后有如下代码：

```
unique_ptr<string> ps;
ps = demo("Uniquely special");
```

这里，`demo()` 返回一个临时的 `unique_ptr`，然后 `ps` 接管原本由返回的 `unique_ptr` 所拥有的对象的所有权。随后，返回的 `unique_ptr` 被销毁。这没有问题，因为 `ps` 现在拥有该 string 对象的所有权。但还有一件好事发生了。由于 `demo()` 返回的临时 `unique_ptr` 很快被销毁，因此不可能被误用来访问无效数据。换言之，在这种情况下没有理由禁止赋值。而且，足够神奇的是，编译器确实允许这样做！

简而言之，如果编译器试图将一个 `unique_ptr` 赋给另一个，当源对象是临时右值时编译器允许，而当源对象具有一定生存期时则不允许：

```
using namespace std;
unique_ptr<string> pu1(new string("Hi ho!"));
unique_ptr<string> pu2;
pu2 = pu1;                              // #1 not allowed
unique_ptr<string> pu3;
pu3 = unique_ptr<string>(new string("Yo!")); // #2 allowed
```

赋值 #1 会留下一个悬空的 `unique_ptr`（即 `pu1`），这可能成为隐患。赋值 #2 不会留下 `unique_ptr`，因为它调用 `unique_ptr` 构造函数，构造一个临时对象，该临时对象在所有权转移给 `pu3` 时被销毁。这种有选择的行为表明 `unique_ptr` 优于 `auto_ptr`，后者会允许两种赋值形式。这也是 `auto_ptr` 对象被禁止（通过建议而非编译器）用于容器对象，而 `unique_ptr` 对象被允许的原因。如果容器算法试图对 `unique_ptr` 对象容器的内容执行类似赋值 #1 的操作，就会得到编译期错误。如果算法试图执行类似赋值 #2 的操作，则没问题，程序会继续执行。对于 `auto_ptr` 对象，像赋值 #1 这样的情况可能导致未定义行为和神秘崩溃。

当然，你可能确实想执行类似语句 #1 的操作。只有当你以不明智的方式使用被弃置的智能指针（例如解引用它）时，赋值才不安全。但你可以通过给它赋新值来安全地复用该指针。C++ 有一个名为 `std::move()` 的标准库函数，可以让你将一个 `unique_ptr` 赋给另一个。下面是一个使用先前定义的 `demo()` 函数（它返回一个 `unique_ptr<string>` 对象）的示例：

```
using namespace std;
unique_ptr<string> ps1, ps2;
ps1 = demo("Uniquely special");
ps2 = move(ps1);                       // enable assignment
ps1 = demo("and more");
cout << *ps2 << *ps1 << endl;
```

你可能想知道，`unique_ptr` 与 `auto_ptr` 不同，如何能够区分安全用法和可能不安全的用法。答案是它使用了 C++11 新增的移动构造函数和右值引用，如第 18 章所述。

此外，`unique_ptr` 还有另一个优于 `auto_ptr` 的优点。它有一个可用于数组的变体。记住，必须将 `delete` 与 `new` 配对，将 `delete []` 与 `new []` 配对。`auto_ptr` 模板使用 `delete`，而不是 `delete []`，因此它只能用于 `new`，不能用于 `new []`。但 `unique_ptr` 有一个 `new[]`、`delete[]` 版本：

```
std::unique_ptr<double[]> pda(new double[5]);  // will use delete []
```

> **注意**
>
> 对于由 `new` 分配的内存，你只应使用 `auto_ptr` 或 `shared_ptr` 对象，而不应用于由 `new []` 分配的内存。对于不是通过 `new` 分配的内存，或者对于 `unique_ptr` 而言不是通过 `new` 或 `new[]` 分配的内存，你不应使用 `auto_ptr`、`shared_ptr` 或 `unique_ptr`。

## 选择智能指针

应该使用哪种指针类型？如果程序使用多个指针指向一个对象，`shared_ptr` 是您的选择。例如，你可能有一个指针数组，并使用一些辅助指针来标识特定元素，例如最大和最小元素。或者你可能有两种对象，它们包含指向同一个第三对象的指针。或者你可能有一个指针的 STL 容器。许多 STL 算法包含复制或赋值操作，这些操作适用于 `shared_ptr`，但不适用于 `unique_ptr`（会得到编译器警告）或 `auto_ptr`（会得到未定义行为）。如果你的编译器不提供 `shared_ptr`，你可以从 Boost 库获取一个版本。

如果程序不需要多个指针指向同一对象，`unique_ptr` 就可以工作。对于返回由 `new` 分配内存的指针的函数，它是返回类型的好选择。这样，所有权被转移给接收返回值的 `unique_ptr`，而该智能指针承担调用 `delete` 的责任。你可以将 `unique_ptr` 对象存储在 STL 容器中，前提是不调用会复制或将一个 `unique_ptr` 赋给另一个的方法或算法，例如 `sort()`。例如，假设有适当的包含和 using 语句，如下代码片段可用于程序中：

```
unique_ptr<int> make_int(int n)
{
    return unique_ptr<int>(new int(n));
}
void show(unique_ptr<int> & pi)                // pass by reference
{
    cout << *pi << ' ';
}
int main()
{
...
vector<unique_ptr<int> > vp(size);
for (int i = 0; i < vp.size(); i++)
    vp[i] = make_int(rand() % 1000);    // copy temporary unique_ptr
vp.push_back(make_int(rand() % 1000));  // ok because arg is temporary
for_each(vp.begin(), vp.end(), show);    // use for_each()
...
}
```

对 `push_back()` 的调用可以工作，因为它传递一个临时 `unique_ptr`，以赋值给 `vp` 中的一个 `unique_ptr`。另请注意，如果 `show()` 按值而不是按引用传递对象，`for_each()` 语句会失败，因为那样就需要用 `vp` 中的一个非临时 `unique_ptr` 初始化 `pi`，这是不允许的。如前所述，编译器会捕获不恰当使用 `unique_ptr` 的尝试。

你可以在与将一个 `unique_ptr` 赋给另一个相同的条件下，将一个 `unique_ptr` 赋给 `shared_ptr`——源必须是右值。和前面一样，在下面的代码中，`make_int()` 是一个返回类型为 `unique_ptr<int>` 的函数：

```
unique_ptr<int> pup(make_int(rand() % 1000));  // ok
shared_ptr<int> spp(pup);                       // not allowed, pup is an lvalue
shared_ptr<int> spr(make_int(rand() % 1000));  // ok
```

`shared_ptr` 模板包含一个显式构造函数，用于将右值 `unique_ptr` 转换为 `shared_ptr`。`shared_ptr` 接管原先由该 `unique_ptr` 拥有的对象的所有权。

你会在与 `unique_ptr` 相同的情形中使用 `auto_ptr`，但后者更受青睐。如果你的编译器不提供 `unique_ptr`，你可以考虑 Boost 库中的 `scoped_ptr`，它类似。

## 标准模板库

STL 提供了一组表示容器、迭代器、函数对象和算法的模板。容器是一个单元，像数组一样，可以保存多个值。STL 容器是同质的；也就是说，它们保存的值全都属于同一类型。算法是完成特定任务的配方，例如对数组排序或在列表中查找特定值。迭代器是让你遍历容器的对象，就像指针让你遍历数组一样；它们是泛化的指针。函数对象是像函数一样行动的对象；它们可以是类对象或函数指针（包括函数名，因为函数名充当指针）。STL 让你构造各种容器，包括数组、队列和列表，并让你执行各种操作，包括搜索、排序和随机化。

Alex Stepanov 和 Meng Lee 在惠普实验室开发了 STL，并于 1994 年发布了实现。ISO/ANSI C++ 委员会投票将其纳入 C++ 标准的一部分。STL 并不是面向对象编程的示例。相反，它代表了一种不同的编程范式，称为泛型编程。这使得 STL 无论是就其功能还是就其方法而言都很有趣。

