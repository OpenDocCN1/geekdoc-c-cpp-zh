
```cpp
#include <iostream>
using namespace std;

class Shape
{
public:
    virtual double Area() = 0;
    virtual void Print() = 0;
    virtual ~Shape() {}
};

class Circle : public Shape
{
    const double Pi;
    double radius;
public:
    Circle(double InputRadius) : radius(InputRadius), Pi(3.1416) {}
    double Area() override
    {
        return 2*Pi*radius;
    }
    void Print() override
    {
        cout << "Circle object" << endl;
    }
};

class Triangle : public Shape
{
    double side;
public:
    Triangle(double InputSide) : side(InputSide) {}
    double Area() override
    {
        return 0.5 * side * side;
    }
    void Print() override
    {
        cout << "Triangle object" << endl;
    }
};

int main()
{
    Shape* shape;
    shape = new Circle(5.0);
    shape->Print();
    cout << "Area: " << shape->Area() << endl;
    delete shape;

    shape = new Triangle(10.0);
    shape->Print();
    cout << "Area: " << shape->Area() << endl;
    delete shape;

    return 0;
}
```

- 2. 转换运算符 `int()` 如下：

```cpp
class Date
{
    int day, month, year;
public:
    Date(int d, int m, int y) : day(d), month(m), year = {} // 等等，让我们修复逻辑
};
```

*实际上，根据提供的 OCR 文本：*

```cpp
class Date
{
    int day, month, year;
public:
    explicit operator int ()
    {
        return (year * 10000) + (month * 100) + day;
    }
};
```

- 2. 下所示的移动构造函数和移动赋值运算符：

```cpp
class DynIntegers
{
    private:
        int* arrayNums;

    public:
        // 移动构造函数
        DynIntegers(DynIntegers&& moveSrc)
        {
            arrayNums = moveSrc.arrayNums; // 获取所有权
            moveSrc.arrayNums = NULL; // 释放源
        }

        // 移动赋值运算符
        DynIntegers& operator= (DynIntegers&& moveSrc)
        {
            if (this != &moveSrc)
            {
                delete arrayNums; // 释放资源
                arrayNums = moveSrc.arrayNums;
                moveSrc.arrayNums = NULL;
            }
            return *this;
        }

        ~DynIntegers() {delete arrayNums;} // 析构

        // 实现默认构造函数，拷贝构造函数，赋值运算符
};
```

## 练习

- 1. `dynamic_cast` 操作的结果应该始终检查其有效性：

```cpp
void DoSomething(base* pBase)
{
    Derived* objDerived = dynamic_cast<Derived*>(pBase);

    if(objDerived) // 检查有效性
        objDerived->DerivedClassMethod();
}
```

- 2. 当你确定指向的对象是 `Tuna` 类型时，使用 `static_cast`。以列表 13.1 为基础，`main()` 函数如下：

```cpp
int main()
{
    Fish* pFish = new Tuna;
    Tuna* pTuna = static_cast<Tuna*>(pFish);

    // Tuna::BecomeDinner 只有在使用有效的 Tuna* 时才能工作
    pTuna->BecomeDinner();

    // Fish 中的虚析构函数确保了 ~Tuna() 的调用
    delete pFish;

    return 0;
}
```

# 第 14课答案

## 问答

- 1. 一种防止重复或递归包含头文件的预处理结构。

- 2. 4。

- 3. 10 + 10/5 = 10 + 2 = 12。

- 4. 使用括号：

```cpp
#define SPLIT(x) ((x) / 5)
```

## 练习

- 1. 结果如下：

`#define MULTIPLY(a,b) ((a)*(b))`

- 2. 这是问答第 4 题中宏的模板版本：

```cpp
template<typename T> T Split(const T& input)
{
    return (input / 5);
}
```

- 3. `swap` 的模板版本将：

```cpp
template <typename T>
void Swap(T& x, T& y)
{
    T temp = x;
    x = y;
    y = temp;
}
```

- 4. `#define QUARTER(x) ((x)/4)`

- 5. 模板类定义如下：

```cpp
template<typename Array1Type, typename Array2Type>
class TwoArrays
{
private:
    Array1Type Array1 [10];
    Array2Type Array2 [10];
public:
    Array1Type& GetArray1(int Index) {return Array1[Index];}
    Array2Type& GetArray2(int Index) {return Array2[Index];}
};
```

- 6. 这是一个包含 `Display()` 函数的完整示例，该函数展示了变长参数及其用法：

```cpp
#include <iostream>
using namespace std;

void Display()
{
}

template <typename First, typename...Last> void Display(First a, Last... U)
{
    cout << a << endl;
    Display(U..);
}

int main()
{
    Display('a');
    Display(3.14);
    Display('a', 3.14);
    Display('z', 3.14567, "The power of variadic templates!");

    return 0;
}
```

## 输出

a

3.14

a

3.14

z

3.14567

The power of variadic templates!

# 第 15课答案

## 问答

- 1. `std::deque`。只有 `deque` 既模拟了动态数组又允许在容器的头部和尾部进行常时间插入。`std::vector` 不允许在开头插入，因此不适用。

- 2. 如果你有键值对，使用 `std::set` 或 `std::map`。如果元素需要重复，则应选择 `std::multiset` 或 `std::multimap`。

- 3. 当你实例化 `std::set` 时，可以可选地提供一个二元谓词模板参数，`set` 类将其作为排序准则。

- 4. 迭代器（Iterators）是算法和容器之间的桥梁，使得算法可以在不需要知道每种容器类型的情况下在各种容器上工作。

- 5. `hash_set` 不是 C++ 标准容器，因此你不应该在任何需要移植性的应用程序中使用它。请使用 `std::map`。

# 第 16课答案

## 问答

- 1. `std::basic_string<T>`

- 2. 将两个字符串拷贝到两个对象中。将每个字符串转换为小写或大写。

- 3. 不，C 风格字符串实际上是指向字符数组的指针，而 STL 字符串类实现了各种运算符和成员函数，使得字符串操作和处理尽可能简单。

## 练习

- 1. 使用 `std::reverse()`：

```cpp
#include <string>
#include <iostream>
#include <algorithm>

int main (){
    using namespace std;

    cout << "请输入一个单词检查回文:" << endl;
    string strInput;
    cin >> strInput;

    string strCopy(strInput);
    reverse(strCopy.begin(), strCopy.end());

    if (strCopy == strInput)
        cout << strInput << " 是回文!" << endl;
    else
        cout << strInput << " 不是回文。" << endl;

    return 0;
}
```

- 2. 使用 `std::find()`：

```cpp
#include <string>
#include <iostream>

using namespace std;

// 在字符串 "strInput" 中查找字符 'chToFind' 的数量
int NumCharacters(string& strInput, char chToFind) {
    int nCharactersFound = 0;

    size_t nCharOffset = strInput.find(chToFind);
    while (nCharOffset != string::npos) {
        ++nCharactersFound;
        nCharOffset = strInput.find(chToFind, nCharOffset + 1);
    }

    return nCharactersFound;
}

int main () {
    cout << "请输入一个字符串:" << endl;
    string strInput;
    getline(cin, strInput);

    int nVowels = NumCharacters(strInput, 'a');
    nVowels += NumCharacters(strInput, 'e');
    nVowels += NumCharacters(strInput, 'i');
    nVowels += NumCharacters(strInput, 'o');
    nVowels += NumCharacters(strInput, 'u');

    cout << "该句子中的元音数量为:" << nVowels << endl;

    return 0;
}
```

- 3. 使用 `toupper()` 函数：

```cpp
#include <string>
#include <iostream>
#include <algorithm>

int main () {
    using namespace std;

    cout << "请输入一个要转换为大写的字符串:" << endl;
    string strInput;
    getline(cin, strInput);

    for (size_t nCharIndex = 0; nCharIndex < strInput.length(); nCharIndex++) {
        strInput[nCharIndex] = toupper(strInput[nCharIndex]);
    }

    cout << "转换为大写的字符串为:" << endl;
    cout << strInput << endl;

    return 0;
}
```

- 4. 这可以简单地通过：

```cpp
#include <string>
#include <iostream>

int main () {
    using namespace std;

    const string str1 = "I";
    const string str2 = "Love";
    const string str3 = "STL";
    const string str4 = "String";

    string strResult = str1 + " " + str2 + " " + str3 + " " + str4;

    cout << "句子内容为:" << endl;
    cout << strResult;

    return 0;
}
```

- 5. 使用 `std::string::find()`：

```cpp
#include <iostream>
#include <string>

int main() {
    using namespace std;

    string sampleStr("Good day String! Today is beautiful!");
    cout << "字符串为: " << sampleStr << endl;
    cout << "查找所有字符 'a' 的实例" << endl;

    auto charPos = sampleStr.find('a', 0);
    while (charPos != string::npos) {
        cout << " 'a' 位于位置: " << charPos << endl;

        // 让 'find' 函数从下一个字符开始向前搜索
        size_t charSearchPos = charPos + 1;
        charPos = sampleStr.find('a', charSearchPos);
    }

    return 0;
}
```

## 输出

字符串为: Good day String! Today is beautiful!

查找所有字符 'a' 的实例

'a' 位于位置: 6

'a' 位于位置: 20

'a' 位于位置: 28

# 第 17课答案

## 问答

- 1. 不，不能。元素只能在 vector 序列的尾部（结尾）以常时间添加。

- 2. 再 10 个。在第 11 次插入时，你会触发重新分配内存。

- 3. 删除最后一个元素；即移除尾部的元素。

- 4. `Mammal` 类型。

- 5. 通过 (a) 下标运算符 `[]` (b) 函数 `()`。

- 6. 随机访问迭代器（Random-access iterator）。

## 练习

- 1. 方案如下：

```cpp
#include <vector>
#include <iostream>
using namespace std;

char DisplayOptions () {
    cout << "你想做什么?" << endl;
    cout << "选择1: 输入一个整数" << endl;
    cout << "选择2: 根据索引查询值" << endl;
    cout << "选择3: 显示 vector" << endl;
    cout << "选择4: 退出!" << endl;

    char ch;
    cin >> ch;
    return ch;
}
```
