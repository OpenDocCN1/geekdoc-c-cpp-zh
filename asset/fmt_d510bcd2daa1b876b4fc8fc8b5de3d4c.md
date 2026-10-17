
```cpp
            largest = num;

    }

    else

        goodNum = false;       // 如果无效

    }

    return goodNum;

}

/**

 * SimpleStat::isLargest

 */

bool SimpleStat::isLargest(int num)

{

    if (num > largest)

        return true;

    else

        return false;

}

/**

 * SimpleStat::calcAverage

 */

double SimpleStat::calcAverage()

{

    if (count > 0)

        return static_cast<double>(sum) / count;

    else

        return 0;

}
```

## 程序 7-8（继续）

```cpp
// 客户端程序

int main()

{

    int num;

    SimpleStat statHelper;

    cout << "\n输入一组非负整数\n";

    cout << "以计算平均值。用空格隔开\n";

    cout << "并在最后一个数字后输入 -1。\n\n";

    cin >> num;

    while (num >= 0) {

        statHelper.addNumber(num);

        cin >> num;

    }

    cout << "\n输入了 " << statHelper.getCount() << " 个数字。\n";

    cout << "\n最大值是 " << statHelper.getLargest() << endl;

    cout << "\n平均值是 " << statHelper.calcAverage() << endl;

    return 0;

}
```

### 加粗显示示例输入的程序输出

请输入一组非负整数
以计算平均值。用空格隔开
并在最后一个数字后输入 -1。

**7 6 8 9 7 7 8 9 -1**

输入了 10 个数字。
最大值是 9
平均值是 7.6

## 将对象传递给函数

概念：类对象可以作为参数传递给函数。

在第 6 章中，你学习了如何使用变量作为函数参数。类对象也可以作为参数传递给函数。例如，以下函数有一个接收 `Rectangle` 对象的参数。

```cpp
void displayRectangle(Rectangle r) {
  cout << "Length = " << r.getLength() << endl;
  cout << "Width = " << r.getWidth() << endl;
  cout << "Area = " << r.calcArea() << endl;
}
```

以下代码创建了一个长度为 15、宽度为 10 的 `Rectangle` 对象，然后将其传递给 `displayRectangle` 函数。

```cpp
Rectangle box(15, 10);
displayRectangle(box);
```

假设 `Rectangle` 类包含了示例中使用的成员函数，`displayRectangle` 函数将输出以下信息：

- Length = 15
- Width = 10
- Area = 150

对于普通变量，对象可以通过值传递或引用传递给显示函数。在 `Rectangle` 示例中，`box` 是通过值传递给 `displayRectangle` 的。这意味着 `displayRectangle` 接收了 `box` 的拷贝。如果使用了任何 `Rectangle` 类的修改函数（mutator），它们只会改变 `box` 的拷贝而不是原始对象。如果函数需要存储或更改对象成员变量中的数据，则必须通过引用传递对象传递。

程序 7-9 说明了这一点。它包含两个接收 `InventoryItem` 对象的函数。对象通过引用传递给 `storeValues` 的，因为该函数需要调用类修改器以将新值存储到对象中。对象通过值传递给 `showValues` 的，因为该函数只需要使用访问器函数来检索并使用对象数据成员中的值。注意程序 7-9 中，`InventoryItem` 类的声明出现在 `storeValues` 和 `showValues` 函数原型之前。这是非常重要的。因为这两个函数都将 `InventoryItem` 作为参数，编译器在遇到任何引用它的内容之前，必须知道 `InventoryItem` 是什么。否则将发生错误。

## 第 7 章 类与对象简介

### 程序 7-9

```cpp
1 // 此程序将对象传递给函数。它通过引用传递给一个函数，
2 // 通过值传递给另一个函数。
3 #include <iostream>
4 #include <iomanip>
5 #include <string>
6 using namespace std;

8 class InventoryItem
{
10 private:
11 int partNum; // 零件编号
12 string description; // 物品描述
13 int onHand; // 库存数量
14 double price; // 单位单价

16 public:

18 void storeInfo(int p, string d, int cH, double cost); // 原型

20 int getPartNum()
{ return partNum; }

23 string getDescription()
{ return description; }

26 int getOnHand()
{ return onHand; }

29 double getPrice()
{ return price; }
};

33 // InventoryItem 类函数 storeInfo 的实现代码
34 void InventoryItem::storeInfo(int p, string d, int cH, double cost)
{ partNum = p;
description = d;
onHand = cH;
price = cost;
}

41 客户端程序的函数原型
42 void storeValues(InventoryItem&); // 通过引用接收对象
43 void showValues(InventoryItem); // 通过值接收对象
```

（程序继续）

### 程序 7-9（续）

```cpp
/******************************************
int main()
{
    InventoryItem part;      // part 是一个 InventoryItem 对象
    storeValues(part);
    showValues(part);
    return 0;
}

/******************************************
* 此函数将用户输入的数据存储在通过引用传递给
* 它的 InventoryItem 对象的成员中。
/**************************************************/
void storeValues(InventoryItem &item)
{
    int partNum;           // 用于持有用户输入的局部变量
    string description;
    int qty;
    double price;
    // 从用户处获取数据
    cout << "Enter data for the new part number\n";
    cout << "Part number: ";
    cin >> partNum;
    cout << "Description: ";      // 跳过上一次输入留在缓冲区中的 '\n'
    cin.get();               
    getline(cin, description);
    cout << "Quantity on hand: ";
    cin >> qty;
    cout << "Unit price: ";
    cin >> price;
    // 将数据存储在 InventoryItem 对象中
    item.setInfo(partNum, description, qty, price);
}

/******************************************
* showValues
* 此函数显示存储通过值传递给它的
* InventoryItem 对象中的成员数据。
/*************************************************/
void showValues(InventoryItem item)
{
    cout << fixed << setprecision(2) << endl;
    cout << "Part Number: " << item.getPartNum() << endl;
    cout << "Description: " << item.getDescription() << endl;
    cout << "Units on Hand: " << item.getOnHand() << endl;
    cout << "Price: " << item.getPrice() << endl;
}
```

### 程序 7-9（续）

#### 示例输出

- Part number: 175
- Description: Hammer
- Quantity on hand: 12
- Unit price: 49.99

#### 常量引用

在程序 7-9 中，对象是通过值传递的。然而，通过值传递对象需要进行拷贝，这会降低执行速度，特别是当对象有很多成员时。通过引用传递对象通常更好，因为不需要拷贝。要将参数声明为常量，必须在函数原型和头文件中放入 `const` 关键字。示例如下：

```cpp
void showValues(const InventoryItem&); // 函数原型
void showValues(const InventoryItem& item) // 函数头
```

```cpp
double getPrice() const
```

7.9 将对象传递给函数

如果 `showValues` 调用任何修改函数，将发生编译错误。注意 `showValues` 已修改为常量引用。

### 从函数返回对象

正如函数可以写为返回 `int`、`double` 或其他数据类型，它们也可以设计为返回对象。事实上，你以前从函数返回过 `string`，因为 `string` 是一个对象。当函数返回对象时，它会创建一个类的局部实例，设置其数据成员，然后将其返回。这实际上展示了 7-9 中使用的 `InventoryItem` 对象如何在 `storeValues` 函数中创建并返回给 `main`。注意此新版本的 `storeValues` 函数不接受任何参数，且其返回类型是 `InventoryItem` 而不是 `void`。

```cpp
InventoryItem storeValues() {
    InventoryItem tempItem; // 局部 InventoryItem 对象
    int partNum; // 用于持有用户输入的局部变量
    string description;
    int qty;
    double price;
    // 此处从用户处获取数据
    // 将数据存储在 InventoryItem 对象中并返回。
    tempItem.storeInfo(partNum, description, qty, price);
    return tempItem;
}
```

`main` 函数可以这样创建 `part`：

```cpp
InventoryItem part = storeValues();
```

程序 7-10 修改了程序 7-9，采用了我们刚刚讨论的技术。以前名为 `storeValues` 的函数重命名为 `createItem`，因为它现在创建 `InventoryItem` 对象并返回给 `main`。`showValues` 函数现在通过常量引用接收 `part`，而不是像那样通过值传递。

### 程序 7-10

```cpp
1 // 此程序使用常量引用参数。
2 // 它还展示了如何从函数返回对象。
3 #include <iostream>
4 #include <iomanip>
5 #include <string>
6 using namespace std;
```

# 第 7 章 类与对象介绍

# 程序 7-10（续）

```cpp
class InventoryItem
{
    private:
    int partNum;            // 零件号
    string description;    // 物品描述
    int onHand;             // 库存数量
    double price;           // 单价
    public:
    void storeInfo(int p, string d, int oH, double cost); // 原型声明
    int getPartNum() const   // 这些函数都已完成
        { return partNum; }  // const 函数。这些确保它们
                             // 不能修改任何类成员数据。
    string getDescription() const
        { return description; }
    int getOnHand() const
        { return onHand; }
    double getPrice() const
        { return price; }
}

// InventoryItem 类函数 storeInfo 的实现代码
void InventoryItem::storeInfo(int p, string d, int oH, double cost)
{
    partNum = p;
    description = d;
    onHand = oH;
    price = cost;
}

// 客户端程序的函数原型声明
InventoryItem createItem();
void showValues(const InventoryItem&); // 接收一个 Inventory
                               // 对象的引用
/**********************/
    main
/**********************/
int main()
{
    InventoryItem part = createItem();
    showValues(part);
    return 0;
}
```

（程序继续）

# 程序 7-10（续） 7.9 将对象传递给函数

```cpp
/*****************************************************
*                                createItem             *
* 此函数将用户输入的数据存储在局部定义的 *
* InventoryObject 对象的成员中，然后返回它。 *
/****************************************************/
InventoryItem createItem()
{
    InventoryItem tempItem; // 本地 Inventory 对象
    int partNum;               // 用于存储用户数据的局部变量
    string description;
    int qty;
    double price;
    // 从用户处获取数据
    cout << "Enter data for the new part number \n";
    cout << "Part number: ";
    cin >> partNum;
    cout << "Description: ";
    // 通过最后一次输入将 '\n' 向左移动
    // 输入缓冲区
    getline(cin, description);
    cout << "Quantity on hand: ";
    cin >> qty;
    cout << "Unit price: ";
    cin >> price;
    // 将数据存储在 InventoryItem 对象中并返回
    tempItem.storeInfo(partNum, description, qty, price);
    return tempItem;
}
```
