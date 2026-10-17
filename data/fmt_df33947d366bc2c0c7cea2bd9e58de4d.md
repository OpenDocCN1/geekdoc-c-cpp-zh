
```cpp
struct fPredicate {
    bool operator< (const WordProperty& lsh, const WordProperty& rsh) const {
        return (lsh.word < rsh.word);
    }
};
```

- 3. 参考第 19课中类似解决的练习题 3。“STL Set 类.”

# 第 21课的答案

## 测验

- 1. 一个一元谓词。

- 2. 它可以显示数据，例如，或者仅仅计算元素。参见列表 21.6 中 `std::transform()` 配合谓词 `tolower()` 的用法。

- 3. 程序运行期间的所有内容都是对象。在这种情况下，即使是结构体和类也可以被当作函数使用，因此被称为函数对象。注意，函数也可以通过函数指针可用——这些也是函数对象。

## 练习题

### 1. 解决方案

```cpp
template <typename elementType=int>
struct Double
{
    void operator () (const elementType element) const
    {
        cout << element * 2 << ' ';
    }
}
```

这个一元谓词可以用于：

```cpp
#include<vector>
#include<iostream>
#include<algorithm>
using namespace std;
```

```cpp
cout << "正在显示整数向量: " << endl;
```

```cpp
// 显示整数数组
for_each(numsInVec.begin(), // 范围开始
    numsInVec.end(), // 范围结束
    Double<>() ); // 一元函数对象
```

```cpp
return 0;
}
```

### 2. 添加一个成员整数，每次使用 `operator ()` 时它都会递增：

```cpp
template <typename elementType=int>
struct Double
{
    int usageCount;

// 构造函数
Double () : usageCount (0) {};
void operator () (const elementType element) const
{
    ++ usageCount;
    cout << element * 2 << ' ';
}
};
```

# 第 22课的答案

### 3. 二元谓词如下：

```cpp
template <typename elementType>
class SortAscending{
public:
    bool operator () (const elementType& num1,
                   const elementType& num2) const
{
        return (num1 < num2);
    }
}
```

这个谓词可以用于：

```cpp
#include<iostream>
#include<vector>
#include<algorithm>
int main() {
    std::vector<int> numsInVec = {100, 90...};
    // 插入示例数字：
    for (int sample = 10; sample > 0; --sample)
        numsInVec.push_back(sample * 10);
    std::sort(numsInVec.begin(), numsInVec.end(), SortAscending<int>());
    return 0;
}
```

## 测验

- 1. Lambda 总是以 `[]` 开始。

- 2. 通过捕获列表 `[Var1, Var2, ...]` `(Type& param) { ...; }`。

- 3. 如下：

```cpp
[Var1, Var2, ...] (Type& param) -> ReturnType { ...; }
```

## 练习题

### 1. Lambda 的一种解决方案是：

```cpp
sort(container.begin(),container.end(),
 [auto el1, auto el2] {return el1 > el2});
```

在练习题 2 解决方案提供的代码中演示了这一点。

### 2. Lambda 看起来是这样的：

```cpp
cout << "你想添加所有元素的数字: ";
int numInput = 0;
cin >> numInput;
for_each(vecNumbers.begin(), numsNumbers.end(),
 [int& element] {element += numInput;});
```

示例演示了练习题 1 和 2 的解决方案：

```cpp
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

template <typename T>
void DisplayContents(const T& container)
{
    for (auto element = container.begin();
         element != container.rend();
         ++element)
        cout << *element << ' ';
    cout << endl;
}

int main()
{
    vector<int> vecNumbers{25, -5, 122, 101};
    DisplayContents(vecNumbers);

    sort(vecNumbers.begin(), numsNumbers.end());
    DisplayContents(vecNumbers);

    sort(vecNumbers.begin(), numsNumbers.end(),
         [](int Num1, int Num2) {return (Num1 > Num2);});
    DisplayContents(vecNumbers);

    cout << "你想添加所有元素的数字: ";
    int numInput = 0;
    cin >> numInput;
    // (此处逻辑根据原文可能不完整，保持结构对应)
```

*(注：原文提供的最后部分似乎存在截断或重复，已按原文结构翻译)*

```cpp
int main() {
    // 将 bitset 初始化为 1001
    std::bitset<4> fourBits(9);

    std::cout << "fourBits: " << fourBits << std::endl;

    // 初始化另一个 bitset 为 0010
    std::bitset<4> fourMoreBits(2);

    std::cout << "fourMoreBits: " << fourMoreBits << std::endl;

    std::bitset<4>addResult(fourBits.to_ulong() + fourMoreBits.to_ulong());
    std::cout << "The result of the addition is: " << addResult;

    return 0;
}
```

2. 对上述示例中的任何一个 bitset 对象调用 `flip()` 函数：

```cpp
addResult.flip();
std::cout << "The result of the flip is: " << addResult << std::endl;
```

# 第 26 课答案

## 测验

- 1. 我会查看 `www.boost.org`。希望你也会这样做！

- 2. 不，通常编写良好（且选择正确）的智能指针不会这样做。

- 3. 当采用侵入式时，它们所拥有的对象需要持有它；否则，它们可以将此信息存储在自由存储上的共享对象中。

- 4. 列表需要双向遍历，因此它需要是双向链表。

## 练习题

- 1. `object->DoSomething() ;` 是错误的，因为指针在之前的拷贝步骤中丢失了对对象的所有权。这将导致崩溃（发生非常不愉快的情况）。

- 2. 代码 own如下：

```cpp
#include <memory>
#include <iostream>
using namespace std;

class Fish {
public:
    Fish() { cout << "Fish: Constructed!" << endl; }
    ~Fish() { cout << "Fish: Destructed!" << endl; }

    void Swim() const { cout << "Fish swims in water" << endl; }
};

class Carp : public Fish {
};

void MakeFishSwim(const unique_ptr<Fish>& inFish) {
    inFish->Swim();
}

int main() {
    unique_ptr<Fish> myCarp(new Carp); // 注意这里
    MakeFishSwim(myCarp);

    return 0;
}
```

鉴于 `MakeFishSwim()` 接受参数作为引用，不涉及拷贝步骤，因此不存在切片问题。此外，注意变量 `myCarp` 的实例化语法。

- 3. `unique_ptr` 不允许拷贝或赋值，因为拷贝构造函数和拷贝赋值运算符都是私有的。

# 第 27 课答案

## 测验

- 1. 使用 `ofstream` 仅写入文件。

- 2. 你应该使用 `cin.getline()`。参见列表 27.7。

- 3. 你不需要这样做，因为 `std::string string` 包含文本信息，你可以保持默认模式，即文本模式（不需要二进制模式）。

- 4. 为了检查 `open()` 是否成功。如果失败，你可能想要显示错误并暂停文件处理。

## 练习题

- 1. 你打开了文件，但在使用流或关闭它之前没有使用 `is_open()` 检查 `open()` 是否成功。

- 2. 你不能向 `ifstream` 插入内容，它是为输入而非输出设计的，因此不支持流插入运算符 `<<`。

# 第 28 课答案

## 测验

- 1. 该类与其他任何类一样，但它是专门创建的作为 `bad_alloc` 等某些异常类的基类。

- 2. `std::bad_alloc`

- 3. 这是一个坏主意，因为异常最初也可能是由于内存不足而抛出的。

- 4. 使用与你可以用于 `bad_alloc` 相同的 `catch (std::exception& exp)`。

## 练习题

- 1. 永远不要在析构函数中抛异常。

- 2. 你忘记了让代码安全（缺少 catch 块块）。

- 3. 不要在 `catch` 块中分配内存！假设 `try` 块中分配的数据丢失并继续。

# 第 29 课答案

## 测验

- 1. 看起来应用程序在一个线程内执行所有操作。因此，如果图像处理本身是计算密集，UI 将无响应。你应该将这两个操作拆分为两个线程，以便操作系统在 UI 和工作线程之间切换时间。

- 2. 你的线程可能同步不当。你同时对对象进行写入和读取，导致数据不一致或损坏。插入一个二进制信号量，确保在被修改时无法访问。

# 索引

# 符号

- `+` (加法运算符),88–89, 347–349

- `+=` (赋值运算符),442–443

- `<` (角括号),19

- `=` (赋值运算符),87, 357–360

- `\` (反斜杠),76–78, 86

- `&` (按位“与”运算符),100–102, 624

- `>>` (按位右移运算符),102–104

- `~` (按位取反运算符),100–102

- `|` (按位“或”运算符),100–102, 624

- `^` (按位异异运算符),100–102, 624

- `{}` (大括号),48, 87

- `:` (冒号),10, 232

- `//` (注释语法),23, 28

- `/*` (注释语法),23, 28

- `?` (条件运算符),126–127

- `--` (递减运算符),89, 190–193, 338–341

- `*` (解引用运算符),183–185, 344–345, 639

- `.` (点运算符),218–219

- `/` (除法运算符),88–89

- `%` (取模运算符),88–89

- `==` (相等运算符),92, 352

- `>>` (提取运算符),27, 624, 649, 663

- `>` (大于运算符),92–94, 354–357

- `>=` (大于等于运算符),92–94, 354–357

- `!=` (不等于运算符),92, 352

- `++` (递增运算符),89, 191–193, 338–341, 26, 624, 662

- `<` (小于运算符),354–357

- `<=` (小于等于运算符),92–94, 354–357

- `&&` (逻辑“与”运算符),95–100

- `||` (逻辑“或”运算符),95–100

- `!` (逻辑“非”运算符),95–100

- `->` (成员选择运算符),219–220, 344–345, 635, 639

- `*` (乘法运算符),88–89

- `()` (括号),364–365, 398–399

- `&` (引用运算符),179–180

- `>>=` (右移运算符),624

- `[]` (下标运算符),197–198, 360–364, 555

- `~` (波浪运算符),234, 451–452

- `::` (作用域解析运算符),225

- `;` (分号),12, 86, 216

- `'` (单引号),45

- `-` (减法运算符),88–89, 347–349

- `0x` (前缀),671

- `\0` (字符串结束字符),76–78, 82

- 内存分配。参见动态内存分配

- ASCII (信息交换标准代码) 代码,41, 711–715

- 美国标准代码为 (ASCII) 代码,41, 711–715

- AND 运算符按位“与” (&),100–102, 624

- 逻辑“与” (&),95–100

- 角括号 (<),19

- `app` 类,661

- `app` 常量,661

- `append()`,442–443

- 区域 (Area),152–153, 158–159

- 参数 `assert()`,399–400

- 赋值运算符 (*),87, 357–360。参见复合赋值运算符

- 关联容器,423–428

- 常量,661

- `auto` 关键字,12–13, 48–50, 172–172, 493

- `auto_ptr` 类,640–643

# 条件代码编译

解释, 346

`function ()`, 364–365

移动赋值, 365–371

移动构造函数, 365–371

关系运算符, 354–357

下标 (1), 360–364

二元谓词, 263, 547–550

`hsearch()`, 573, 592–595

位, 703

`bitset` 类, 622–627, 706

位运算运算符, 100–104, 624

块, 87, 117–118

`bool` 类型, 40

布尔型变量, 声明, 40

Boost 线程库, 645, 690

括号 ( ), 81–140

`break` 语句, 139–n`break` 方法, 705

缓冲区, 507

`bug`, 8

字节, 703

准则与禁忌, 388

`dynamic_cast` 运算符, 381–384

解释, 377

必要性, 378

问题, 386–387

`reinterpret_cast` 运算符, 384–385

`static_cast` 运算符, 380–381

上转型, 380

友元类, 258–260

实例化, 217–218

禁止在栈上实例化, 249–251

命名规范, 219

确保对象不可拷贝性, 246

`private` 关键字, 220–224

`public` 关键字, 222–222

允许拷贝, 237–240

单例类, 247–249

`sizeof ()`, 255–257

子类, 275

父类, 275

## 捕获异常

所有异常, 673–674

`catch` 关键字, 673–675

示例, 617–679

异常类型, 674–675

内存分配失败, 202–204

`try` 关键字, 673

联合体, 260–266

`clear()`, 472–483

`Clone()`, 638

CodeGuru, 699

CodeProject, 699

集合, 插入元素, 597–599

冲突, 529

冒号 (), 10

注释, 18, 23, 28

编译, 10–12, 13, 709–710

编译时检查, 编译错误, 14

条件代码编译, 697–698

示例, 10–12

## C

`.c` 文件扩展名, 9

`c_str()`, 440

## C++

年龄, 6

演变, 7

历史, 6

新特性, 12–13

愿景, 12–13

`t++`, 699, 559–560

捕获列表, `case`, 449–450

敏感性 0, 398

类型转换

`const_cast` 运算符, 385–386

C 风格强制转换, 379

`bgen()`, 442
