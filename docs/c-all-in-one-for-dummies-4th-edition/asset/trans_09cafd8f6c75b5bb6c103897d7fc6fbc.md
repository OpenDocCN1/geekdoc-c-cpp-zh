
为了确保它能正常工作，以下内容可以放入 `main()` 中：

```cpp
StringArray OrigList = new PChar[3];
OrigList[0] = "John";
OrigList[1] = "Paul";
OrigList[2] = "George";

StringArray CopyList = OrigList;
ChangeAsReference(OrigList);

cout << OrigList[0] << endl;
cout << OrigList[1] << endl;
cout << OrigList[2] << endl;
cout << CopyList[0] << endl;
cout << CopyList[1] << endl;
cout << CopyList[2] << endl;
```

这段代码创建一个指向包含三个字符串的数组的指针。然后在该数组中存储三个字符串。接下来，代码将指针的副本保存到名为 `CopyList` 的变量中，通过调用 `ChangeAsReference()` 修改 `OrigList` 指针，并打印所有值。输出如下：

```
Tom
Suzy
Harry

John
Paul
George
```

前三个输出是 `OrigList` 中的元素，它们被传入了 `ChangeAsReference()`。它们不再具有 John、Paul 和 George 这些值。三个原始名称已被三个新名称取代：Tom、Harry 和 Suzy。然而，`CopyList` 变量仍然指向原始字符串列表。因此，修改指针引用再次奏效。

## 使用指针处理字符串数组

上一节使用 typedef 来处理字符串数组，但也可以使用指针来实现。下面是该函数的修改版本，这次使用上述指针（如 Pointer04 示例所示）：

```cpp
void ChangeAsPointer(StringArray *array) {
    StringArray NameArray = new PChar[3];
```

## 函数指针

当应用程序运行时，应用程序中的函数存在于内存中；因此，就像内存中的其他任何内容一样，它们也有地址。

你可以通过取得函数名并在函数名前放置取地址运算符（&）来访问函数的地址，如下所示：

```
address = &MyFunction;
```

但要做到这一点，你需要知道将 address 声明为什么类型。address 变量是指向函数的指针，而指定类型最干净的方法是使用 auto，如下所示：

```
auto address = &MyFunction;
```

传统方法是使用 typedef（如 FunctionPointer01 示例所示）。下面是你需要的 typedef：

```
typedef int(*FunctionPtr)(int);
```

这很难理解，这也是使用 auto 更好的原因，但新类型的名称是 FunctionPtr。这定义了一个名为 FunctionPtr 的类型，它返回一个整数（最左侧的 int），并接受一个整数作为参数（最右侧的 int，必须放在括号中）。该语句中间部分是新类型的名称，并且必须在其前面加一个星号，表示它是指向表达式其余所有内容的指针。此外，必须将类型名及其前面的星号放在括号内。现在可以声明一些变量了！如下所示：

```
FunctionPtr address = &MyFunction;
```

这一行将 address 声明为指向函数的指针，并将其初始化为 MyFunction()。要使其工作，MyFunction() 的代码必须具有 typedef 中声明的相同原型：在这种情况下，它必须接受一个整数作为参数并返回一个整数。因此，例如，你可能有一个这样的函数：

```
int TheSecretNumber(int x) {
  return x + 1;
}
```

然后可以有一个 `main()`，它将该函数的地址存入一个变量，然后通过该变量调用函数：

```cpp
int main() {
  typedef int (*FunctionPtr)(int);
  int MyPasscode = 20;
  FunctionPtr address = &TheSecretNumber;
  cout << address(MyPasscode) << endl;
}
```

使用 `typedef` 方法的优点是能精确指定你希望的输入形式，但 auto 形式更短、更易理解。下面是使用 auto 形式的 `main()`（必须使用 C++ 11 或以上版本才能使用这种形式）：

```cpp
int main() {
  int MyPasscode = 20;
  auto address = &TheSecretNumber;
  cout << address(MyPasscode) << endl;
}
```

为了让你可以说自己见过这种写法，下面是不使用 `typedef` 时地址声明会是什么样子：

```cpp
int (*address)(int) = &TheSecretNumber;
```

关键特征是：括号内并排有两样东西，右边那组里面只有类型。左边那组有一个变量名。因此这一行不是在声明类型，而是在声明变量。

## 将变量指向方法

使用面向对象编程（OOP）时，需要一种访问对象内方法的方式。在对象的代码中，使用 `this` 指针获取对象方法的地址，以便可以直接访问方法的实例数据。

请记住，类的每个实例都有自己的属性副本，除非属性是静态的。但方法在整个类中共享。是的，你可以区分静态方法和非静态方法。但这样做只是指它们所访问的变量类型不同：静态方法只能访问静态属性，而且不需要通过实例来引用它们。非静态（即普通、常规）方法则与特定实例一起工作。然而，在内存中，实际上只存在方法的一份副本。

那么方法如何知道要处理哪个实例呢？`this` 参数会被传入方法，以区分不同实例。假设有一个名为 Gobstopper 的类，其中有一个名为 `Chew()` 的方法。接着有一个名为 MyGum 的实例，你像这样调用 `Chew()` 方法：

```cpp
MyGum.Chew();
```

当编译器为此生成汇编代码时，它实际上会向函数传入一个参数——MyGum 实例的地址，也称为 `this` 指针。因此代码中只有一个 `Chew()` 函数，但要调用它，必须使用该类的特定实例。

因为内存中只有 `Chew()` 方法的一份副本，所以可以获取它的地址。但这样做需要一些看起来晦涩的代码。下面直接给出。假设你的类如下所示：

```cpp
class Gobstopper {
public:
    int WhichGobstopper;
    int Chew(string name) {
        cout << WhichGobstopper << endl;
        cout << name << endl;
        return WhichGobstopper;
    }
};
```

`Chew()` 方法接受一个字符串并返回一个整数。下面是指向 `Chew()` 函数的指针的 typedef：

```cpp
typedef int (Gobstopper::*GobMember)(string);
```

下面是一个 `GobMember` 类型的变量：

```cpp
GobMember func = &Gobstopper::Chew;
```

与其他函数一样，在使用 C++11 或更高版本时，可以使用 `auto` 来简化操作。下面是使用 `auto` 形式、指向 `Chew()` 方法的变量：

```cpp
auto func = &Gobstopper::Chew;
```

如果仔细看这个 typedef，它看起来与常规函数指针相似。唯一区别是类名和两个冒号位于星号之前。除此之外，它就是一个普通的旧式函数指针。

![](img/128ab511de4e7360e167e3b15cdd5dd0_526_0.png)

但是，常规函数指针仅限于指向具有特定参数类型集合和返回类型的函数，而这个函数指针同样受这些限制，并且还有进一步限制：它只能指向 `Gobstopper` 类内的方法。

要调用存储在指针中的函数，需要有一个特定实例。注意，在前面代码中对 `func` 的赋值里没有实例，只有类名和函数 `&Gobstopper::Chew`。因此要调用该函数，先取得一个实例，加上 `func`，然后调用即可！FunctionPointer02 示例（如清单 1–2 所示）包含一个完整示例，其中有该类、方法地址和两个独立实例。

### 清单 1-2：获取方法的地址

```cpp
#include <iostream>

using namespace std;

class Gobstopper {
public:
    int WhichGobstopper;
    int Chew(string name) {
        cout << WhichGobstopper << endl;
        cout << name << endl;
        return WhichGobstopper;
    }
};

int main() {
    typedef int (Gobstopper::*GobMember)(string);
    GobMember func = &Gobstopper::Chew;

    Gobstopper inst;
    inst.WhichGobstopper = 10;

    Gobstopper another;
    another.WhichGobstopper = 20;

    (inst.*func)("Greg W.");
    (another.*func)("Jennifer W.");
    return 0;
}
```

