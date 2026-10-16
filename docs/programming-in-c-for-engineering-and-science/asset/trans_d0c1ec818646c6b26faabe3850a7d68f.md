

## 12.5 示例：搜索化学数据库

### 12.5.1 问题

一个数据文件包含无机化合物的信息，这些信息以连续成对的行形式存放——一行是名称，下一行是化学式和比热（使物体温度升高 1°C 所需的热量与使等质量水温度升高 1°C 所需的热量之比）。需要开发一个查表程序，允许用户输入化学式，然后在化学式列表中搜索该化学式，并显示与该化学式对应的名称和比热。

### 12.5.2 解决方案

#### 12.5.2.1 初步分析

一种做法是使用上一章中的文件处理功能——打开文件，逐行读取，直到找到包含所需化学式的行，在屏幕上显示该行，然后关闭文件。如果我们只打算搜索一个或少数几个化学式，这种方法是可以接受的。然而，从辅助存储器中的文件检索信息比在主存储器中处理数据要慢得多，因此对于大量搜索来说，反复打开和关闭文件并从头搜索可能过于耗时，尤其是在文件很大的情况下。

显而易见的解决方案是，对文件进行一次遍历，将各项复制到主存储器中的独立数组中，以便快速处理。但是，我们应该给这些数组多大的容量？如果太小，无法存储所有数据；如果太大，又会浪费太多内存。我们需要的是一个可以随着我们添加项而增长的数组，正如我们将在下一节中看到的，这就是 `vector<T>` 对象能做到的。因此，我们将使用以下对象来存储文件中的数据：

-   formula：`vector<string>` 对象，用于存储化学式
-   name：`vector<string>` 对象，用于存储名称
-   specificHeat：`vector<float>` 对象，用于存储比热

示例 12.3 中的程序展示了此类 `vector<T>` 对象的用处。它实现了以下算法：

-   1. 打开文件，读取化学式、名称和比热，并分别存储到 formula、name 和 specificHeat 中。
-   2. 重复以下步骤，直到用户为 aFormula 输入 “QUIT”：
    -   a. 输入 aFormula。
    -   b. 如果 aFormula == “QUIT”，终止重复；否则继续以下步骤：
    -   c. 搜索以在 formula 中找到 aFormula 的位置，或确定它不存在。
-   d. 如果找到 aFormula，显示 name 和 specificHeat 中第 location 个元素。否则，显示一条 "Not Found" 信息。

## 示例 12.3 搜索化学数据库

```
/* Program to read a file containing the name, formula, and specific heat for various inorganic compounds and store these in vector<T> objects. The user then enters various formulas; the list of formulas is searched for each; if found, its name and specific heat are displayed.

Input(keyboard): name of data file and formulas (or "QUIT")
Input(file):     chemical formulas, names, and specific heats
Output(screen):  Prompts for formulas; if found, name and specific heat displayed; otherwise, a "not found" message
--------------------------------------------------------------------------*/

#include <iostream>                // cin, cout, >>, <<
#include <fstream>                 // ifstream
#include <cassert>                 // assert()
#include <string>                  // string, getline()
#include <vector>                  // vector<T>
using namespace std;

int main()
{
    cout << "Program reads chemical formulas until user enters QUIT.\n"
         "For each formula, it searches a list of formulas, and if\n"
         "the formula is found, the name and specific heat of that\n"
         "inorganic compound is displayed; otherwise,'Not Found' "
         "is displayed.\n\n";

    // Open an input stream to the file
    cout << "Enter the name of the input file: ";
    string inputFileName;
    getline(cin, inputFileName);
    ifstream inStream;
    inStream.open(inputFileName.data());
    assert( inStream.is_open() );

    // Copy contents of file into 3 vector<T>s
    string aFormula, name1, name2;
    float aSpecificHeat;
    vector<string> formula, name;
    vector<float> specificHeat;

for (;;)
{
    inStream >> name1 >> name2;
    inStream >> aFormula >> aSpecificHeat;
    if ( inStream.eof() ) break;
    name.push_back(name1 + " " + name2);
    formula.push_back(aFormula);
    specificHeat.push_back(aSpecificHeat);
}
inStream.close();

// Retrieve information about formulas for user
for(;;)
{
    cout << "\nEnter a formula (QUIT to stop): ";
    cin >> aFormula;
    if (aFormula == "QUIT" || aFormula == "quit") break;
    int location = 0;
    bool found = false;
    while (location < formula.size() && formula[location] != aFormula)
        location++;
    found = (location < formula.size());
    if (found)
        cout << "Name: " << name[location]
             << " Spec. Heat: " << specificHeat[location] << endl;
    else
    {
        cout << aFormula << " == not found\n";
        cout << "Would you like a list of formulas (Y or N)? ";
        char response;
        cin >> response;
        if (response == 'Y' || response == 'y')
            for (int i = 0; i < formula.size(); i++)
                cout << formula[i] << endl;
    }
}
```

### chemFile.txt 文件清单：

-   Silver Chloride
-   AgCl 0.0804
-   Aluminum Chloride
-   AlCl3 0.188
-   Gold Iodide
-   AuI 0.0404
-   Barium Carbonate
-   BaCO3 0.0999
-   Calcium Carbonate
-   CaCO3 0.203
-   Calcium Chloride
-   CaCl2 0.1604
-   Ferric Oxide
-   Fe2O3 0.182
-   Hydrogen Peroxide
-   H2O2 0.471
-   Potassium Chloride
-   KCl 0.162
-   Lithium Fluoride
-   LiF 0.373
-   Sodium Bromide
-   NaBr 0.118
-   Sodium Chloride
-   NaCl 0.204
-   Lead Bromide
-   PbBr2 0.0502
-   Silicon Carbide
-   SiC 0.143
-   Stannous Chloride
-   SnCl2 0.162
-   Zinc Sulfate
-   ZnSO4 0.174

### 示例运行：

```
Program reads chemical formulas until user enters QUIT.
For each formula, it searches a list of formulas, and if the formula is found, the name and specific heat of that inorganic compound is displayed; otherwise, 'Not Found' is displayed.

Enter the name of the input file: chemFile.txt

Enter a formula (QUIT to stop): NaCl
Name: Sodium Chloride Spec. Heat: 0.204

Enter a formula (QUIT to stop): PBR
PBR == not found
Would you like a list of formulas (Y or N)? Y
AgCl
AlCl3
AuI
BaCO3
CaCO3
CaCl2
Fe2O3
H2O2
KCl
LiF
NaBr
NaCl
PbBr2
SiC
SnCl2
ZnSO4

Enter a formula (QUIT to stop): PbBr2
Name: Lead Bromide Spec. Heat: 0.0502
  .
Enter a formula (QUIT to stop): QUIT
```

在下一节中，我们将详细考察 `vector<T>` 类模板。

## 12.6 vector<T> 类模板

### 12.6.1 函数模板快速回顾

在 10.6 节中，我们介绍了函数模板，它们是函数的模式，编译器可以根据这些模式创建实际的函数定义。模板通常有一个类型参数，用作函数调用时将要提供的类型的占位符。例如，我们考虑了以下函数模板：

```
template <typename Item>
void swap(Item & first, Item & second)
{
    Item temporary = first;
    first = second;
    second = temporary;
}
```

当使用以下参数调用 `swap()` 时：

```
swap(int1, int2);
```

编译器会创建 `swap()` 的一个实例，其中类型参数 `Item` 被替换为 `int`——即变量 `int1` 和 `int2` 的类型。但是当 `swap()` 被 char 值 `ch1` 和 `ch2` 调用时：

```
swap(ch1, ch2);
```

编译器会创建 `swap()` 的一个实例，其中 `Item` 被替换为 `char`。因此，函数模板允许程序员创建泛型函数——与类型无关的函数。

### 12.6.2 vector<T> 类模板

除了函数模板之外，C++ 还允许类模板，类模板是与类型无关的模式，可以从中定义实际的类。这些模板对于构建泛型容器类——存储其他对象的对象——很有用。在 20 世纪 90 年代初，惠普实验室的 Alex Stepanov 和 Meng Lee 用一套有用的类和函数模板库扩展了 C++，这个库后来被称为标准模板库（STL），并且是标准 C++ 库之一。

STL 中最简单但非常有用的一种容器是 `vector<T>` 类模板，可以将其视为一种与类型无关的独立数组类模式，其容量可以改变。`vector<T>` 对象的声明可以有以下形式：

| 声明 | 说明 |
|---|---|
| `vector<type> v;` | 构造容量为 0 的 v，其元素类型为指定类型 |
| `vector<type> v(n);` | 构造容量为 n 的 v，其元素类型为指定类型 |
| `vector<type> v(n, initVal);` | 将 v 构造为容量为 n 的 `vector<type>`，其元素类型为指定类型，并初始化为 initVal |

例如，对于声明

```
vector<string> formula, name;
vector<float> specificHeat;
```

在示例 12.3 的程序中，`vector<string>` 和 `vector<float>` 是由 `vector<T>` 模板形成的类。这些声明创建了两个名为 `formula` 和 `name` 的 `vector<string>` 对象，以及一个名为 `specificHeat` 的 `vector<float>` 对象，这意味着 `formula` 和 `name` 可以存储 string 值，`specificHeat` 可以存储 float 值。最初，这些对象的容量和大小均为零。如果我们希望开始时对象具有非零容量，可以在名称后面附加常量；例如，

```
vector<float> specificHeat(10);
```

创建 `vector<float>` 对象 `specificHeat`，但其内部数组已预先分配了容量 10。如果我们希望用某个初始值填充这些数组元素，可以在此声明中添加第二个值；例如，

```
vector<float> specificHeat(10, 0);
```

会将 `specificHeat` 的每个数组元素初始化为 0。这里，我们只关注较简单的形式，因为正如示例 12.3 中的程序所展示的，从容量 0 开始通常不是问题，因为与必须在编译时知道容量的 C 风格数组不同，`vector<T>` 对象的空间是在程序执行期间分配的，并且可以在必要时扩展。

