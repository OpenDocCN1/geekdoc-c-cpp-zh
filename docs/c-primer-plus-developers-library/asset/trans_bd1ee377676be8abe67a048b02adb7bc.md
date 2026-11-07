
程序清单8.6中的程序正是做了这些事情。它还通过让函数返回结构的引用，增加了一个有趣的变数。这与返回结构的工作方式略有不同。有一些注意事项需要留意，我们稍后会讨论。

## 程序清单8.6 **strc_ref.cpp**

```cpp
//strc_ref.cpp -- using structure references
#include <iostream>
#include <string>
struct free_throws
{
    std::string name;
    int made;
    int attempts;
    float percent;
};

void display(const free_throws & ft);
void set_pc(free_throws & ft);
free_throws & accumulate(free_throws & target, const free_throws & source);

int main()
{
// partial initializations - remaining members set to 0
    free_throws one = {"Ifelsa Branch", 13, 14};
    free_throws two = {"Andor Knott", 10, 16};
    free_throws three = {"Minnie Max", 7, 9};
    free_throws four = {"Whily Looper", 5, 9};
    free_throws five = {"Long Long", 6, 14};
    free_throws team = {"Throwgoods", 0, 0};
// no initialization
    free_throws dup;

    set_pc(one);
    display(one);
    accumulate(team, one);
    display(team);
// use return value as argument
    display(accumulate(team, two));
    accumulate(accumulate(team, three), four);
    display(team);

// use return value in assignment
    dup = accumulate(team,five);
    std::cout << "Displaying team:\n";
    display(team);
    std::cout << "Displaying dup after assignment:\n";
    display(dup);
    set_pc(four);
    // ill-advised assignment
    accumulate(dup, five) = four;
    std::cout << "Displaying dup after ill-advised assignment:\n";
    display(dup);
    return 0;
}

void display(const free_throws & ft)
{
    using std::cout;
    cout << "Name: " << ft.name << '\n';
    cout << "  Made: " << ft.made << '\t';
    cout << "Attempts: " << ft.attempts << '\t';
    cout << "Percent: " << ft.percent << '\n';
}
void set_pc(free_throws & ft)
{
    if (ft.attempts != 0)
        ft.percent = 100.0f * float(ft.made)/float(ft.attempts);
    else
        ft.percent = 0;
}

free_throws & accumulate(free_throws & target, const free_throws & source)
{
    target.attempts += source.attempts;
    target.made += source.made;
    set_pc(target);
    return target;
}
```

以下是程序输出：

```text
Name: Ifelsa Branch
  Made: 13    Attempts: 14    Percent: 92.8571
Name: Throwgoods
  Made: 13    Attempts: 14    Percent: 92.8571
Name: Throwgoods
  Made: 23    Attempts: 30    Percent: 76.6667
Name: Throwgoods
  Made: 35    Attempts: 48    Percent: 72.9167
Displaying team:
Name: Throwgoods
  Made: 41    Attempts: 62    Percent: 66.129
Displaying dup after assignment:
Name: Throwgoods
```

那么返回值呢？我们刚才讨论的函数调用没有使用它；就这种用法而言，该函数本可以是`void`类型。但看看这个函数调用：

```cpp
display(accumulate(team, two));
```

这里发生了什么？让我们追踪结构对象`team`。首先，`team`作为第一个参数传递给`accumulate()`。这意味着`accumulate()`中的目标对象实际上就是`team`。`accumulate()`函数修改`team`，然后将其作为引用返回。请注意，实际的返回语句如下：

```cpp
return target;
```

这条语句中没有任何信息表明返回的是一个引用。这些信息来自函数头（也来自原型）：

```cpp
free_throws & accumulate(free_throws & target, const free_throws & source)
```

如果返回类型声明为`free_throws`而不是`free_throws &`，同样的返回语句将返回`target`的一个副本（因此也是`team`的副本）。但返回类型是引用，所以这意味着返回值是最初传递给`accumulate()`的原始`team`对象。

接下来会发生什么？`accumulate()`的返回值是`display()`的第一个参数，所以这意味着`team`是`display()`的第一个参数。由于`display()`的参数是引用，所以`display()`中的`ft`对象实际上就是`team`。因此，`team`的内容会被显示出来。最终效果

```cpp
display(accumulate(team, two));
```

与下面的代码效果相同：

```cpp
accumulate(team, two);
display(team);
```

同样的逻辑也适用于这条语句：

```cpp
accumulate(accumulate(team, three), four);
```

这与下面的代码效果相同：

```cpp
accumulate(team, three);
accumulate(team, four);
```

接下来，程序使用了一条赋值语句：

```cpp
dup = accumulate(team, five);
```

正如你所预料的，这会将`team`中的值复制到`dup`。

最后，程序以另一种并非本意的方式使用了`accumulate()`：

```cpp
accumulate(dup, five) = four;
```

这条语句——也就是将值赋给函数调用——之所以能工作，是因为返回值是一个引用。如果`accumulate()`按值返回，这段代码将无法编译。由于返回值是对`dup`的引用，这段代码的效果与下面的代码相同：

```cpp
accumulate(dup,five); // 把five的数据添加到dup
dup = four; // 用four的内容覆盖dup的内容
```

第二条语句抹除了第一条语句完成的工作，因此最初的赋值语句并不是对`accumulate()`的良好使用。

### 为什么要返回引用？

让我们进一步看看返回引用与传统返回机制有何不同。后者的工作原理与函数参数按值传递非常相似。`return`后面的表达式被求值，然后该值被传回调用函数。从概念上讲，这个值会被复制到一个临时位置，然后调用程序使用这个值。考虑以下代码：

```cpp
double m = sqrt(16.0);
cout << sqrt(25.0);
```

在第一条语句中，值4.0被复制到一个临时位置，然后该位置的值被复制到m。在第二条语句中，值5.0被复制到一个临时位置，然后该位置的内容被传递给cout。（这是概念性的描述。在实践中，优化编译器可能会合并其中的一些步骤。）

现在考虑这条语句：

```cpp
dup = accumulate(team,five);
```

如果`accumulate()`返回的是结构而不是结构的引用，这可能需要将整个结构复制到一个临时位置，然后将该副本复制到`dup`。但使用引用返回值时，`team`直接复制到`dup`，这是一种更高效的方式。

> **注意**
>
> 返回引用的函数实际上是所引用变量的别名。

### 注意返回引用所引用的对象

返回引用时要记住的最重要的一点是，避免返回对函数终止时就不再存在的内存位置的引用。你需要避免的是下面这类代码：

```cpp
const free_throws & clone2(free_throws & ft)
{
    free_throws newguy;    // 走向大错误的第一步
    newguy = ft;           // 复制信息
    return newguy;         // 返回对副本的引用
}
```

这会产生一个不幸的后果：返回对临时变量（newguy）的引用，而该变量在函数终止时立刻不复存在。（第9章“内存模型和命名空间”讨论了各种变量的持续性。）同样，你应该避免返回指向这类临时变量的指针。

避免这个问题的最简单方法是返回作为参数传递给函数的引用。引用参数将引用调用函数使用的数据；因此，返回的引用也将引用相同的数据。例如，这正是`accumulate()`在程序清单8.6中所做的。

第二种方法是使用`new`创建新的存储空间。你已经见过一些例子，其中`new`为字符串创建空间，函数返回指向该空间的指针。下面是如何用引用做类似的事情：

```cpp
free_throws & clone(free_throws & ft)
{
    free_throws * pt;        // 复制信息
    *pt = ft;                // 返回对副本的引用
    return *pt;
}
```

第一条语句创建了一个匿名的free_throws结构。指针`pt`指向该结构，所以`*pt`就是该结构。代码看起来像是返回结构，但函数声明表明该函数实际上返回的是对这个结构的引用。然后你可以这样使用该函数：

```cpp
free_throws & jolly = clone(three);
```

这使`jolly`成为新结构的引用。这种方法有一个问题：当内存不再需要时，应该使用`delete`释放由`new`分配的内存。调用`clone()`隐藏了对`new`的调用，使得之后更容易忘记使用`delete`。第16章“string类和标准模板库”中讨论的`auto_ptr`模板，或者更确切地说，C++11的`unique_ptr`，可以帮助自动完成删除过程。

### 为什么在返回引用时使用const？

你可能还记得，程序清单8.6中有这样一条语句：

```cpp
accumulate(dup,five) = four;
```

它的效果是先将来自five的数据添加到dup，然后用four的内容覆盖dup的内容。为什么这条语句可以编译？赋值要求左侧是一个可修改的左值。也就是说，赋值表达式左侧的子表达式应该标识一块可以被修改的内存。在这种情况下，函数返回了对dup的引用，而dup确实标识了这样一块内存。因此该语句是有效的。

另一方面，普通（非引用）返回类型是右值，是无法通过地址访问的值。这类表达式可以出现在赋值语句的右侧，但不能出现在左侧。右值的其他示例包括字面量（如`10.0`）和表达式（如`x + y`）。显然，试图取得像`10.0`这样的字面量的地址是没有意义的，但为什么普通的函数返回值是右值呢？这是因为，你回想一下，返回值位于一个临时的内存位置，这个位置甚至不一定能保留到下一条语句。
