

关键在于，计算机无法做出这个决定；你需要选择希望数据以何种方式呈现。在你决定了排序方式之后，就可以创建一个函数，用于判断一条记录何时小于、等于或大于另一条记录。如果你希望列表按姓名排序，就应该让函数只关注姓名。但如果你希望列表按社会保险号排序，就应该编写一个比较社会保险号的函数。

清单6-7中展示的 Maps3 示例包含一个 map 类，其中带有一个用于判断两个键是否相等的比较函数。

### 清单6-7：包含实例并需要比较它们的函数

```cpp
#include <iostream>
#include <map>

using namespace std;

class Emp {
public:
    string Nickname;
    string SSN;

    Emp(string anickname, string asocial) :
        Nickname(anickname),
        SSN(asocial) {}

    Emp() : Nickname(""), SSN("") {}
};

class Salary {
public:
    int YearlyInc;
    int Taxes;

    Salary(int annual, int adeductions) :
        YearlyInc(annual),
        Taxes(adeductions) {}

    Salary() : YearlyInc(0), Taxes(0) {}
};

bool operator < (const Emp& first, const Emp& second) {
    return first.Nickname < second.Nickname;
}

int main() {
    map<Emp, Salary> employees;

    Emp emp1("sparky", "123-22-8572");
    Salary sal1(135000, 18);
    employees[emp1] = sal1;

    Emp emp2("buzz", "234-33-5784");
    Salary sal2(150000, 23);
    employees[emp2] = sal2;

    // Now test it out!
    Emp emptest("sparky", "");
    cout << employees[emptest].YearlyInc << endl;
    return 0;
}
```

运行这个应用程序时，你会看到 Salary 值中的 YearlyInc 成员，该值的键是名为 sparky 的 Employee 对象：

```text
135000
```

现在请注意这段代码中的几点。首先，要查找 Sparky 的薪水，你并不需要 Sparky 的 Employee 实例。相反，你创建一个 Employee 实例并设置 Nickname 成员，而无需关心 SSN 成员。然后使用 map 的方括号表示法来获取值：

```cpp
cout << employees[emptest].YearlyInc << endl;
```

map 代码使用小于函数来完成这个任务。该 < 函数只比较 Nickname 成员，而不比较 SSN 成员。注意，这个函数必须返回布尔值，并且你需要在 < 前面加上 operator 关键字，从而将其定义为运算符函数——一个定义操作数之间运算的函数。你也可以稍微改变一下做法，像这样比较 SSN 成员：

```cpp
bool operator < (const Emp& first, const Emp& second) {
    return first.SSN < second.SSN;
}
```

然后你就可以根据 SSN 查找 Sparky 的薪水：

```cpp
Emp emptest("", "123-22-8572");
cout << employees[emptest].YearlyInc << endl;
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_673_0.png)

单独一个 `<` 函数似乎不足以执行所有必要的比较，比如相等性比较。然而，代码会调用两次小于函数，第二次会交换参数的顺序；如果两次都返回 false，计算机就会判定它们相等。使用这种方法会让事情变得更简单，因为你只需要提供一个比较函数。

### 理解默认的 `<` 函数

标准库中的容器有一个默认的 `<` 函数。如果你没有提供自己的 `<` 函数，容器就会为你提供这个默认的 `<` 函数。这个默认函数依赖于一个名为 less 的模板类。这个模板很简单：它只包含一个返回布尔值的方法：

```text
x < y
```

对于大多数基本类型，默认函数都能正常工作。例如，当你使用整数时，编译器可以轻松地使用默认函数。然而，在处理自定义类时，编译器无法理解 `<` 运算符，除非你提供自己的 `<` 运算符函数，正如你在本章其他地方看到的那样。但是，由于容器在其参数中接受一个类，且默认为 less 类，你可以编写自己的类并加以使用，而不必编写自己的 `<` 运算符函数。下面是一个示例：

```cpp
class MyLess {
public:
  bool operator()(const MyClass &x, const MyClass &y) const {
    return x.Name < y.Name;
  }
};
```

然后，例如当你创建一个 map 时，可以将这个类作为第三个参数传入，而不是依赖默认参数：

`map<MyClass, MyClass, MyLess> mymap;`

这样你就不需要自己编写小于函数了。这种方法的好处是，你现在拥有一个标准化的 `<` 函数实现，可以在任何地方使用，而且在团队环境中工作时尤其有用。

## 遍历容器

标准库中的容器提供了对容器内容的概览。如果你的容器中装满了对象，你通常只能大致了解里面有什么，但如果能够深入查看细节就更好了。你可以使用*迭代器*来深入容器内部。迭代器与容器配合使用，让你可以逐个对象地遍历容器。接下来的小节将介绍迭代器以及如何使用它们。

### 使用迭代器

每个容器类都包含一个名为 `iterator` 的内嵌类型。你需要使用完全限定名来创建迭代器实例。例如，如果你有一个保存整数和字符串的 map，如 `map<int, string>`，你可以这样创建迭代器实例：

```cpp
map<string, int>::iterator loopy
```

虽然 `loopy` 是 `iterator` 的一个实例，但其中涉及不少类型定义，实际上 `loopy` 是指向容器中存储的某个元素的指针。要将 `loopy` 初始化为指向容器中的第一个元素，需要调用容器的 `begin()` 方法，并将结果存储在 `loopy` 中。然后 `loopy` 就会指向容器中的第一个元素。你可以通过解引用 `loopy` 来访问该元素；处理完后，你可以像这样递增 `loopy` 来移动到下一个元素：

```cpp
loopy++;
```

你可以通过多种方式使用这种技术，例如前面清单6-3中展示的对 `reverse_copy()` 的调用。你可以通过检查 `loopy` 是否指向容器中的最后一个元素来判断是否处理完毕。为此，需要调用容器的 `end()` 方法，并将 `loopy` 与 `end()` 的返回值进行比较。如果相等，就说明处理完了。下面几行代码演示了这些步骤：

```cpp
vector<string>::iterator vectorloop = Words.begin();
while (vectorloop != Words.end())
{
    cout << *vectorloop << endl;
    vectorloop++;
}
```

你可以看到迭代器所使用的类型，这里名为 `vectorloop`，它通过调用 `begin()` 来初始化。对 `vectorloop` 进行解引用以访问数据，然后递增以获取下一个元素。while 循环将 `vectorloop` 与 `end()` 的返回值进行比较，以确定处理何时完成。清单6-8中展示的 Iterators 示例代码给出了一个更完整的迭代器使用示例。

### 清单6-8：迭代

```cpp
#include <iostream>
#include <map>
#include <vector>

using namespace std;

int main() {
    // Iterating through a map
    map<string, int> NumberWords;
    NumberWords["ten"] = 10;
    NumberWords["twenty"] = 20;
    NumberWords["thirty"] = 30;

    map<string, int>::iterator loopy = NumberWords.begin();
    while (loopy != NumberWords.end()) {
        cout << loopy->first << " ";
        cout << loopy->second << endl;
        loopy++;
    }

    // Iterating through a vector
    vector<string> Words;
    Words.push_back("hello");
    Words.push_back("there");
    Words.push_back("ladies");
    Words.push_back("and");
    Words.push_back("aliens");

    vector<string>::iterator vectorloop = Words.begin();
    while (vectorloop != Words.end()) {
        cout << *vectorloop << endl;
        vectorloop++;
    }
    return 0;
}
```

编译并运行这个应用程序后，你会看到以下输出：

