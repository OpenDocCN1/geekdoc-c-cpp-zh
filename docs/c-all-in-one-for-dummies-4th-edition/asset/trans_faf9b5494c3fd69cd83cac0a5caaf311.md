
对 `abi::__cxa_demangle()` 的调用会执行实际的名称还原。你收到的是一个 `unique_ptr`，即 `Result`，其中包含指向该类型人类可读形式的指针。如果 `abi::__cxa_demangle()` 调用不成功，`Result` 将包含一个空指针，你可以返回 "Error" 作为结果，而不是实际的类型字符串。要使这段代码正常工作，需要修改 `DisplayIt()`，如下所示：

```cpp
void DisplayIt(auto Value) {
    cout << Value << " is of the " <<
        DemangleIt(typeid(Value).name()) << " type." << endl;
}
```

现在运行该示例时，你会看到人类可读形式的输出，这会让使用它变得容易得多。

```text
Hello There! is of the char const* type.
Hello Again! is of the std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> > type.
1234 is of the int type.
5678 is of the int type.
12.34 is of the double type.
56.78 is of the float type.
1 is of the bool type.
0 is of the bool type.
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_409_0.png)

此时，你应该会注意到使用 `auto` 的一些情况：你并不总能得到预期的类型。在这个例子中，使用 `auto` 声明的字符串与使用 `string` 声明的字符串类型不同。类型推导过程也常常依赖默认类型。例如，如果你想使用 `float`，却把变量声明为 `auto`，结果会是 `double`，因为那是默认类型。

## 将函数传递给函数

有时你需要对一组数字应用某个处理过程，或者需要对单个数字应用多个处理过程。事实上，有时你需要同时做这两件事。遇到这种情况时，最简单的处理方法是把函数（也就是你想执行的处理过程）传递给另一个负责处理该情况的函数。在接下来的几节中，你会先看到一个简单示例，它使用多个处理过程对单个数字执行这项任务。你还会看到如何通过一种称为*变换*的技术，将单个处理过程应用到一组数字上，因为你是在把一系列数字转换成另一系列数字。

## 查看函数输入的简单示例

有时，单个数字表示一个基准值，但你必须用各种方式处理它才能得到结果。例如，你可能需要找到正确的处理过程，以某个基准值作为起点来优化一组特定的值。清单 1-8 所示的 FunctionFunction 示例演示了如何使用这种技术。

### 清单 1-8：将函数传递给函数

```cpp
#include <iostream>
#include <vector>

using namespace std;

int AddSome(int Value) {
    return Value + 10;
}

int DelSome(int Value) {
    return Value - 10;
}

int MulSome(int Value) {
    return Value * 10;
}

int DivSome(int Value) {
    return Value / 10;
}

typedef int(*FuncPtr)(int);

void ModIt(int Value, vector<FuncPtr> FuncArray) {
    int NumFunc = FuncArray.size();
    cout << "Processing " << NumFunc << " functions."
      << endl;

    for(int i = 0; i < NumFunc; i++)
        cout << FuncArray[i](Value) << endl;
}

int main() {
    vector<FuncPtr> FuncArray =
        {*AddSome, *DelSome, *MulSome, *DivSome};
    ModIt(10, FuncArray);
    return 0;
}
```

在大多数使用这种技术的情况下，你会创建一个函数指针数组或向量。使用向量更灵活，因为你不必预先确定要传递的函数数量——它可以是任意数量，最多达到该向量的最大大小。不过，要让这种技术生效，你必须先创建一个 typedef，用它定义每个函数指针条目的形式，该形式由以下部分组成：

- 返回值，类型为 `int`
- 括号中的函数指针，即 `(*FuncPtr)`
- 括号中的输入参数，即 `(int)`

![](img/128ab511de4e7360e167e3b15cdd5dd0_411_0.png)

typedef（为某种对象类型创建新名称）在本书中出现了不少地方。例如，在第 4 册第 1 章中，你会看到它用于配合向量处理字符串。第 5 册第 1 章演示了如何将 typedef 与多维数组一起使用。事实上，如果你想全面理解 typedef 的所有用途，第 5 册就是该去的地方。

你将向量定义为 `vector<FuncPtr>`，并给它一个向量名，例如 `FuncArray`。接下来创建该向量，就是提供指向本例中用于测试的四个函数的指针：`AddSome()`、`DelSome()`、`MulSome()` 和 `DivSome()`。这四个函数做的事情不多，但它们确实有助于测试。

代码调用 `ModIt()`，传入你想处理的值（这里是 10）以及函数指针向量 `FuncArray`。在 `ModIt()` 内部，代码依次用提供的值调用每个函数，并将结果输出到屏幕上。下面是这个示例的输出：

```text
Processing 4 functions.
20
0
100
1
```

## 使用变换

变换允许你使用单个函数处理一系列值。组合一系列变换，使你能够按特定顺序使用一系列函数处理一系列值。你会看到变换以各种方式被使用，包括对数据做条件处理和处理视频。清单 1-9 所示的 Transform 示例通过 C++ 范围功能概述了这种技术的工作方式。

### 清单 1-9：对一系列数据点使用变换

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct EvenPair {
    int Value;
    bool Even;
};

EvenPair IsEven(int Value){
    if (Value % 2 == 0)
        return EvenPair{Value, true};

    return EvenPair{Value, false};
}

int main(){
    vector<int> Values{1, 2, 3, 4};
    vector<EvenPair> Evens(Values.size());

    transform(Values.begin(), Values.end(),
              Evens.begin(), IsEven);

    for(auto isEven : Evens)
        if (isEven.Even)
            cout << isEven.Value << " is even." << endl;
        else
            cout << isEven.Value << " is odd." << endl;

    return 0;
}
```

这个示例使用 `EvenPair` 结构保存两个变量，其中包含你想检查的原始值，以及该值是否为偶数的显示结果。在 `main()` 中，你先创建两个向量：一个输入向量 `Values`，一个输出向量 `Evens`。`Evens` 向量将包含原始值列表，以及表示每个值是否为偶数的布尔值。

![](img/128ab511de4e7360e167e3b15cdd5dd0_413_0.png)

对 `transform()` 的调用接收指向 `Values` 开头和结尾的指针、指向 `Evens` 开头的指针，以及用于执行变换的函数名。在这个例子中，`IsEven()` 接收单个 `Value`，使用取模运算符 `Value % 2` 判断它是否为偶数，然后输出一个 `Value` 和 `Even` 对。

变换完成后，一个 foreach 循环会检查 `Evens` 中的每个值，并输出相应的字符串。结果如下：

```text
1 is odd.
2 is even.
3 is odd.
4 is even.
```

## 使用 Lambda 表达式实现

lambda 表达式是一种无名函数，可以用来代替常规函数引用。通过将函数内联，使用 lambda 表达式可以让代码更具可读性。本小册的第 2 章和第 3 章会详细介绍 lambda 表达式，但清单 1-10 所示的 Lambda 示例展示了一种替代方式，可以用更短的方式创建清单 1-9 中展示的代码。

### 清单 1-10：使用 Lambda 表达式执行变换

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct EvenPair {
    int Value;
    bool Even;
};

int main(){
  vector<int> Values{1, 2, 3, 4};
  vector<EvenPair> Evens(Values.size());

  transform(Values.begin(), Values.end(),
            Evens.begin(), [](int Value) {
              return (Value % 2 == 0)
                     ? EvenPair{Value, true}
                     : EvenPair{Value, false};});

  for(auto isEven : Evens)
    if (isEven.Even)
      cout << isEven.Value << " is even." << endl;
    else
      cout << isEven.Value << " is odd." << endl;

  return 0;
}
```

这个示例的基本思路与本章前面“使用变换”一节中的示例相同，只是它使用 lambda 表达式代替对 `IsEven()` 的调用。lambda 表达式以捕获子句 `[]` 开头，该子句定义如何捕获任何所需的外部变量。空捕获子句表示该 lambda 表达式只能使用其局部变量，在这里就是 `Value`。

与 `IsEven()` 一样，该 lambda 表达式需要一个 `int` 输入 `Value`。编译器会根据 lambda 表达式代码推导输出类型。不过，在需要时，你可以使用 `-> output_type` 直接指定输出类型。在这种情况下，你会用 `[](int Value) -> EvenPair` 代替所示的代码。

输出是两个值之一，由三目运算符决定。当 `(Value % 2 == 0)` 为真时，输出为 `EvenPair{Value, true}`；否则，输出为 `EvenPair{Value, false}`。重点在于，这个版本比清单 1-9 中的版本更短，因此当你想要使用的函数很小时，lambda 表达式可以让代码更短、更易理解。

