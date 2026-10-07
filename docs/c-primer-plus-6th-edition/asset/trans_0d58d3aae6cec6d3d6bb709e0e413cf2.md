

# 第8章 函数函数的探险

```cpp
set_pc(four);
// 不明智的赋值
accumulate(dup, five) = four;
std::cout << "Displaying dup after ill-advised assignment:\n";
display(dup);
return 0;
}

void display(const free_throws & ft)
{
    using std::cout;
    cout << "Name: " << ft.name << '\n';
    cout << "Made: " << ft.made << '\t';
    cout << "Attempts: " << ft.attempts << '\t';
    cout << "Percent: " << ft.percent << '\n';
}
void set_pc(const free_throws & ft)
{
    if (ft.attempts != 0)
        ft.percent = 100.0*float(ft.made)/float(ft.attempts);
    else
        ft.percent = 0;
}
```

```cpp
free_throws & accumulate(free_throws & target, const free_throws & source)
{
    target.attempts += source.attempts;
    target.made += source.made;
    set_pc(target);
    return target;
}
```

这里是程序的输出：

Name: Ifelsa Branch
Made: 13 Attempts: 14 Percent: 92.8571
Name: Throwgoods
Made: 13 Attempts: 14 Percent: 92.8571
Name: Throwgoods
Made: 23 Attempts: 30 Percent: 76.6667
Name: Throwgoods
Made: 35 Attempts: 48 Percent: 72.9167
Displaying team:
Name: Throwgoods
Made: 41 Attempts: 62 Percent: 66.1290
Displaying dup after assignment:
Name: Throwgoods
Made: 41 Attempts: 62 Percent: 66.129
Displaying up after ill-advised assignment:
Name: Whily Looper
Made: 5 Attempts: 9 Percent: 55.5526

# 程序注释

程序开始时初始化了几个结构体对象。记住，如果初始化器的数量少于成员数量，剩余成员（在本例中只是 `percent` 成员）将被设置为 0。第一个函数调用了它：

```cpp
set_pc(one);
```

由于 `set_pc()` 中的形式参数 `ft` 是一个引用，因此 `ft` 指向 `one`，`set_pc()` 中的代码设置了 `one->percent` 成员。在这种情况下，按值传递将不起作用，因为这将设置 `one` 的临时拷贝的 `percent` 成员。另一种方法（正如你可能从上一章记得的那样）是使用指针参数传递地址，但前者稍微复杂一点：

```cpp
set_pc(&one);    // 使用指针，用 &one 代替 one
```

```cpp
void set_pc(free_throws * pt)
{
    if (pt->attempts != 0)
        pt->percent = 100.0f*float(pt->made)/float(pt->attempts);
    else
        pt->percent = 0;
}
```

下一个函数调用了它：

```cpp
display(one);
```

由于 `display()` 显示结构体的内容而不修改它们，因此该函数使用了 `const` 引用参数。在这种情况下，可以按值传递结构体，但使用引用在时间和内存上比拷贝原始结构体更节省资源。
下一个函数调用了它：

```cpp
accumulate(team, one);
```

`accumulate()` 函数接受两个结构体参数。它将第二个结构体的 `attempts` 和 `made` 成员的数据加到第一个结构体的对应成员中。只有第一个结构体被修改了，因此第一个参数是引用，而第二个参数是 `const` 引用：

```cpp
free_throws & accumulate(free_throws & target, const free_throws & source);
```

# 第8章 函数函数的探险

返回值呢？我们刚刚讨论的那个函数调用没有使用返回值；就我们目前的使用，该函数的类型可以是 `void`。但请看这个函数调用：

```cpp
display(accumulate(team, two));
```

这里发生了什么？让我们跟踪结构体对象 `team`。首先，`team` 作为第一个参数传递给 `accumulate()`。这意味着 `accumulate` 中的 `target` 对象（实际上是 `team`）。`accumulate()` 函数修改了 `team`，然后将其作为引用返回。注意，实际的返回语句看起来如下：

```cpp
return target;
```

该语句中没有任何部分表明正在返回一个引用。该信息来自函数头（并且也来自原型）：
free_throws & accumulate(free_throws & target, const free_throws & source)

如果返回类型声明为 `free_throws` 而不是 `free_throws &`，那么相同的返回语句将返回 `target` 的拷贝（因此是 `team` 的拷贝）。但由于返回类型是引用，这意味着返回值是传递给 `accumulate()` 的原始 `team` 对象。

接下来会发生什么？`accumulate()` 的返回值是 `display()` 的第一个参数，这意味着 `team` 是 `display()` 的第一个参数。由于 `display()` 的参数是引用，这意味着 `display()` 中的 `ft` 对象实际上就是 `team`。因此，`team` 的内容被显示出来。以下

```cpp
display(accumulate(team, two));
```

最终的效果与以下代码相同：

```cpp
accumulate(team, two);
display(team);
```

同样的逻辑也适用于这条语句：

```cpp
accumulate(team, three);
```

它的效果与以下代码相同：

```cpp
accumulate(team, three);
accumulate(team, four);
```

接下来，程序使用了一个赋值语句：

```cpp
dup = accumulate(team, five);
```

正如你预期的，这拷贝了 `team` 中的值。最后，程序以一种它并非设计初衷使用了 `accumulate()`：

```cpp
accumulate(dup, five) = four;
```

这条语句——即给函数调用赋值——之所以能工作，是因为返回值是一个引用。如果 `accumulate()` 按值返回，代码将无法编译。由于返回值是到 `dup` 的引用，这段代码的效果与以下代码相同：

```cpp
accumulate(dup, five); // 将五 的数据加到 dup
dup = four; // 用 four 覆盖 dup 的内容
```

第二条语句抵消了第一条语句完成的工作，因此赋值语句并不是 `accumulate()` 的良好用法。

# 引用变量

让我们进一步观察一下，为什么返回引用与传统的返回机制不同。后者是按值返回。返回引用的不同之处在于：

```cpp
void display(const free_throws & ft) 
{
    using std::cout;
    cout << "Name: " << ft.name << '\n';
    cout << "Made: " << ft.made << '\t';
    cout << "Attempts: " << ft.attempts << '\t';
    cout << "Percent: " << ft.percent << '\n';
}
```

在 `display()` 中，`ft` 是 `const`，所以不能修改 `ft` 的成员。但在下面的例子：

```cpp
void set_pc(const free_throws & ft)
{
    if (ft.attempts != 0)
        ft.percent = 100.0*float(ft.made)/float(ft.attempts);
    else
        ft.percent = 0;
}
```

在 `set_pc()` 中，`ft` 不是 `const` 的，所以可以修改它的成员。而在下面的例子：

```cpp
void set_pc(free_throws * pt)
{
    if (pt->attempts != 0)
        pt->percent = 100.0f*float(pt->made)/float(pt->attempts);
    else
        pt->percent = 0;
}
```

在 `set_pc()` 中，`pt` 是一个指针，所以可以使用 `pt->` 来访问成员。而在下面的例子中：

```cpp
free_throws & accumulate(free_throws & target, const free_throws & source)
{
    target.attempts += source.attempts;
    target.made += source.made;
    set_pc(target);
    return target;
}
```

在 `accumulate()` 中，`target` 不是 `const` 的，所以可以修改它的成员。而 `source` 是 `const` 引用，所以该函数不能修改它的成员。

# 返回引用的危险

返回一个局部变量的引用是非常危险的，因为局部变量在函数结束时就会被销毁。

```cpp
free_throws & get_ft()
{
    free_throws ft;
    return ft;
}
```

在这个例子中，`ft` 是一个局部变量。当函数返回时，`ft` 会被销毁，返回它的引用将将指向一个无效的内存。这会导致未定义行为。

为了避免这种情况，我们可以按值返回：

```cpp
free_throws get_ft()
{
    free_throws ft;
    return ft;
}
```

在这个例子中，`ft` 的拷贝被返回，这样是安全的。

另一种方法是使用堆来分配内存，并返回一个指针：

```cpp
free_throws* get_ft()
{
    free_throws* ft = new free_throws;
    return ft;
}
```

在这个例子中，`ft` 是在堆上分配的，直到它被显式删除。但是，这要求调用者必须使用 `delete`，否则会导致内存泄漏。

在现代 C++ 中，可以使用智能指针来自动管理内存：

```cpp
#include <memory>
std::unique_ptr<free_throws> get_ft()
{
    return std::unique_ptr<free_throws>(new free_throws);
}
```

在这个例子中，`unique_ptr` 会在它离开作用域时自动释放内存。

# 安全的返回引用

返回引用总是总是安全的，只要所引用的对象的生命周期比引用本身长。

```cpp
free_throws & get_ft()
{
    static free_throws ft;
    return ft;
}
```

在这个例子中，`ft` 是静态的，它在整个程序运行期间一直存在，因此返回它的引用是安全的。但是，这种方法在多线程环境下是不安全的。

更安全的方法是返回一个传入的引用：

```cpp
free_throws & get_ft(free_throws & ft)
{
    return ft;
}
```

在这个例子中，`ft` 是由调用者提供的，只要调用者确保它在在使用期间有效，返回它的引用就是安全的。

# 总结

- 函数可以按值、按引用或按指针返回。
- 按值返回通常是安全的。
- 返回引用或指针时必须非常对象的生命周期。
- 返回局部变量的引用是危险的。

# 练习

1.  以下代码会产生什么问题？

```cpp
free_throws & get_ft()
{
    free_throws ft;
    return ft; // 错误！
}
```

```cpp
free_throws* get_ft()
{
    free_throws ft;
    return &ft; // 错误！
}
```

2.  编写一个函数 `copy_ft`，它按值返回一个 `free_throws` 对象。

3.  编写一个函数 `accumulate_ft`，它接收两个 `free_throws` 对象（引用），并将它们的尝试次数相加，返回第一个引用。

4.  编写一个函数 `display_ft`，它接收一个 `free_throws` 对象（`const` 引用）并打印它的内容。

