

这就产生了一个高效且安全的函数调用。它高效是因为只传递了一个引用；向量不会被复制。它安全是因为向量引用的引用是常量引用；`display()` 不能改变 inventory。

## 陷阱

你不能修改标记为常量引用的参数。如果尝试这样做，你会生成编译错误。

接下来，`display()` 使用对 inventory 的常量引用列出向量中的元素。然后控制权返回到 `main()`，程序结束。

## 决定如何传递参数

到目前为止，你已经看到了三种不同的传递参数的方式——按值传递、作为引用传递、作为常量引用传递。那么如何决定使用哪种方法呢？以下是一些指导原则：

- **按值传递。** 当参数变量是基本内置类型之一时，按值传递，例如 `bool`、`int` 或 `float`。这些类型的对象非常小，按引用传递不会带来任何效率提升。你还应该在想要计算机复制变量时按值传递。你可能想要使用副本，如果你计划在函数中更改参数，但又不希望实际的参数变量受到影响。

- **作为常量引用传递。** 当你想高效地传递一个不需要更改的值时，传递常量引用。

- **作为引用传递。** 仅当你想更改参数变量的值时才传递引用。然而，你应该尽可能避免更改参数变量。

## 返回引用

就像传递值一样，当你从函数返回一个值时，你实际上返回的是该值的副本。再次强调，对于基本内置类型的值，这不是什么大问题。然而，如果你返回一个大型对象，这可能是一项昂贵的操作。返回引用是一种高效的替代方案。

## 介绍 Inventory Referencer 程序

Inventory Referencer 程序演示了返回引用。程序通过使用返回的引用来显示包含英雄物品的向量的元素。然后程序通过返回的引用更改其中一个物品。图 6.4 显示了程序的结果。

![](img/34f09be0ed6217c465debc4490197d4f_221_0.png)

### 图 6.4

英雄的物品是通过使用返回的引用来显示和更改的。

你可以从 Course Technology 网站 (www.courseptr.com/downloads) 下载此程序的代码。该程序位于第 6 章文件夹中；文件名是 inventory_referencer.cpp。

```
// Inventory Referencer
// Demonstrates returning a reference

#include <iostream>
#include <string>
#include <vector>

using namespace std;

//returns a reference to a string
string& refToElement(vector<string>& inventory, int i);
```

```
int main()
{
    vector<string> inventory;
    inventory.push_back("sword");
    inventory.push_back("armor");
    inventory.push_back("shield");

    //displays string that the returned reference refers to
    cout << "Sending the returned reference to cout:\n";
    cout << refToElement(inventory, 0) << "\n\n";

    //assigns one reference to another -- inexpensive assignment
    cout << "Assigning the returned reference to another reference.\n";
    string& rStr = refToElement(inventory, 1);
    cout << "Sending the new reference to cout:\n";
    cout << rStr << "\n\n";

    //copies a string object -- expensive assignment
    cout << "Assigning the returned reference to a string object.\n";
    string str = refToElement(inventory, 2);
    cout << "Sending the new string object to cout:\n";
    cout << str << "\n\n";

    //altering the string object through a returned reference
    cout << "Altering an object through a returned reference.\n";
    rStr = "Healing Potion";
    cout << "Sending the altered object to cout:\n";
    cout << inventory[1] << endl;

    return 0;
}

//returns a reference to a string
string& refToElement(vector<string>& vec, int i)
{
    return vec[i];
}
```

## 返回引用

在从函数返回引用之前，你必须指定你正在返回一个引用。这就是我在 `refToElement()` 函数头中所做的。

```
string& refToElement(vector<string>& inventory, int i)
```

通过在指定返回类型时使用引用运算符 `string&`，我表示函数将返回一个字符串对象的引用（而不是字符串对象本身）。你可以使用我这样的方式使用引用运算符来指定函数返回特定类型对象的引用。只需将引用运算符放在类型名称之后即可。

函数 `refToElement()` 的主体只包含一个语句，该语句返回向量中位置 i 的元素的引用。

```
return vec[i];
```

请注意，`return` 语句中没有任何内容表明函数返回引用。函数头和原型决定函数返回对象还是对象的引用。

## 陷阱

尽管返回引用可以高效地将信息发送回调用函数，但你必须小心不要返回对超出作用域对象的引用——一个不再存在的对象。例如，以下函数返回对函数结束后再也不存在的 `string` 对象的引用——这是非法的。

```
string& badReference()
{
    string local = "This string will cease to exist once the function ends.";
    return local;
}
```

避免此类问题的一种方法是永远不要返回对局部变量的引用。

## 显示返回引用的值

在创建 `inventory` 向量后，我通过返回的引用显示第一个物品。

```
cout << refToElement(inventory, 0) << "\n\n";
```

前面的代码调用 `refToElement()`，它返回对 `inventory` 中位置 0 的元素的引用，然后将该引用发送到 `cout`。因此，`sword` 被显示。

## 将返回的引用分配给引用

接下来我用以下行将返回的引用分配给另一个引用，该行将对 `inventory` 中位置 1 的元素的引用分配给 `rStr`。

```
string& rStr = refToElement(inventory, 1);
```

这是高效的赋值，因为将引用分配给引用不涉及对象的复制。然后我将 `rStr` 发送到 `cout`，显示 `armor`。

## 将返回的引用分配给变量

接下来我将返回的引用分配给一个变量。

```
string str = refToElement(inventory, 2);
```

前面的代码并没有将引用分配给 `str`。它不能，因为 `str` 是一个 `string` 对象。相反，代码复制返回的引用所指的元素（`inventory` 中位置 2 的元素），并将该 `string` 对象的副本分配给 `str`。由于这种赋值涉及对象的复制，因此比将一个引用分配给另一个引用更昂贵。有时以这种方式复制对象的成本完全可以接受，但你应该意识到这种赋值相关的额外开销，并在必要时避免它。

接下来我将新的 `string` 对象 `str` 发送到 `cout`，显示 `shield`。

## 通过返回的引用更改对象

你也可以更改返回的引用所指的对象。这意味着你可以通过 `rStr` 更改英雄的物品，如以下代码行所示。

```
rStr = "Healing Potion";
```

由于 `rStr` 引用 `inventory` 中位置 1 的元素，因此此代码将 `inventory[1]` 更改为等于 "Healing Potion"。为了证明这一点，我使用以下行显示该元素，确实显示了 `Healing Potion`。

```
cout << inventory[1] << endl;
```

如果我想保护 `inventory`，以免 `refToElement()` 返回的引用被用来更改向量，我应该将函数的返回类型指定为常量引用。

