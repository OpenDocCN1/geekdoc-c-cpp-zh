
```cpp
// 字段:
char codeA;

// 构造函数:
Alpha(char a) {
    codeA=a;
}

// 虚方法:
virtual void show() {
    cout<<"The method from the class Alpha:"<<
codeA<<endl;
}

// 第二个基类:
class Bravo {
public:
    // 字段:
    char codeB;
    // 构造函数:
    Bravo(char b) {
        codeB=b;
    }

    // 虚方法:
    virtual void show() {
        cout<<"The method from the class Bravo:"<<
codeB<<endl;
    }
};

// 派类:
class Charlie:public Alpha,public Bravo {
public:
    // 空构造函数:
    Charlie(char a, char b):Alpha(a),Bravo(b) {}

// 重写方法:
void show() {
    cout<<"The method from the class Charlie: ";
    cout<<codeA<<codeB<<endl;
}

// 程序的主函数:
int main() {
    cout<<"Using variables\n";
    // 创建对象:
    Alpha objA('A');
    objA.show();
    Bravo objB('B');
    objB.show();
    Charlie objC('C','D');
    objC.show();
    // 将派生类对象
    // 赋值给基类的对象变量:
    objA=objC;
    objB=objC;
    objA.show();
    objB.show();
    cout<<"Using pointers\n";
    // 声明指针:
    Alpha* pntA=&objC;
    Bravo* pntB=&objC;
    Charlie* pntC=&objC;
    // 通过指针调用方法:
    pntA->show();
    pntB->show();
    pntC->show();
    return 0;
}
```

我们从程序中获得了以下输出：

### 程序的输出（见列表 6.11）

```
Using variables
The method from the class Alpha: A
The method from the class Bravo: B
The method from the class Charlie: CD
The method from the class Alpha: C
The method from the class Bravo: D
Using pointers
The method from the class Charlie: CD
The method from the class Charlie: CD
The method from the class Charlie: CD
```

程序需要一些解释。`Alpha` 和 `Bravo` 类是 `Charlie` 类的基类。`Alpha` 类中有一个字符字段 `codeA`、带有一个参数的构造函数以及 `show()` 方法。`show()` 方法是一个虚方法。`Bravo` 类中也存在类似的方法。该类中还有字符字段 `codeB` 和带有一个参数的构造函数。`Charlie` 类继承了 `Alpha` 和 `Bravo` 类。`Charlie` 类构造函数有两个参数。我们将它们传递给基类的构造函数。由于我们没有在构造函数执行执行其他操作，因此构造函数体是空的（大括号内没有语句）。我们重写了 `Charlie` 类的 `show()` 方法，使其打印字段 `codeA` 和 `codeB`。

有趣的地方发生在 `main()` 函数中。我们分别创建了 `Alpha`、`Bravo` 和 `Charlie` 类的对象 `objA`、`objB` 和 `objC`。对于每个对象，我们都调用了 `show()` 方法。然后我们使用语句 `objA=objC` 和 `objB=objC`。根据这些语句，我们将派类 `Charlie` 的对象 `objC` 赋值给基类 `Alpha` 和 `Bravo` 的对象变量 `objA` 和 `objB`。由于 `Charlie` 类派自 `Alpha` 和 `Bravo`，这些赋值是正确的。

然而，通过基类变量，我们只能访问在基类中声明的字段和方法。这就是为什么通过变量 `objA` 调用方法时，我们只能访问字段 `codeA` 和在 `Alpha` 类中定义的 `show()` 方法版本。通过变量 `objB`，我们访问字段 `codeB` 和来自 `Bravo` 类的 `show()` 方法版本。

当我们使用指针时情况发生了变化。在程序中，我们创建了三个指针。它们分别是指向 `Alpha` 类对象的指针 `ptrA`、指向 `Bravo` 类对象的指针 `ptrB` 以及指向 `Charlie` 类对象的指针 `ptrC`。我们通过指针调用了方法。

```cpp
cout<<endl;
}
// 模板函数对数组排序：
template<class X> void sort(X* m,int n) {
    // 打印未排序的数组：
    show(m,n);
    // 模板类型的局部变量：
    X s;
    // 嵌套循环语句：
    for(int i=1;i<=n-1;i++) {
        for(int j=0;j<n-i;j++) {
            if(m[j]>m[j+1]) {
                // 交换元素的值：
                s=m[j+1];
                m[j+1]=m[j];
                m[j]=s;
            }
        }
    }
    // 打印排序后的数组：
    show(m,n);
}
// 程序的主函数：
int main() {
    // 数值数组：
    int A[5]={3,2,8,1,0};
    // 字符数组：
    char B[7]={'Z','B','Y','A','D','C','X'};
    // 对数组排序：
    sort(A,5);
    sort(B,7);
    return 0;
}
```

# 第 7 章 模板函数与类

以下是程序的输出结果：

```
程序的输出（见列表 7.2）

3 2 8 1 0
0 1 2 3 8
Z B Y A D C X
A B C D X Y Z
```

在对模板函数 `show()` 的描述中，我们将类型参数标记为 `T`。该函数有两个参数。第一个参数 `m` 的类型为 `T*`。这意味着参数 `m` 是一个指向相同类型类型值的指针，该类型被“隐藏”在 `T` 之后。这里 `m` 代表一个数组，其元素类型为 `T`。函数 `show()` 的第二个参数 `n` 是一个整数，它决定了传递给数组的大小。我们通过循环语句打印数组 `m` 的元素。

我们描述了带有类型参数 `X` 的用于数组排序的模板函数 `sort()`。该函数没有返回值，与 `show()` 函数一样，它有两个参数。第一个参数 `m` 是指向类型为 `X` 的值的指针。我们假设这是一个类型为 `X` 的元素的数组名。第二个整数 `n` 是数组的大小。在 `sort()` 函数中，我们通过语句 `show(m,n)` 调了模板函数 `show()`。它会打印未排序数组的内容。我们声明了模板类型 `X` 的局部变量 `s`。我们需要这个变量来交换数组中的元素。在完成排序后，我们通过 `show(m,n)` 语句将其打印出来。

在 `main()` 函数中，我们通过 `int A[5]={3,2,8,1,0}` 和 `char B[7]={'Z', 'B', 'Y', 'A', 'D', 'C', 'X'}` 语句创建了整数和字符数组。为了对它们进行排序，我们分别使用了 `sort(A, 5)` 和 `sort(B, 7)` 语句。

> 注意
>
> 比较字符意味着比较它们的编码。

# 带有多个参数的模板函数

一个模板函数可以有多个模板参数。作为说明，让我们考虑列表 7.3 中的程序。

## 列表 7.3. 带有多个参数的模板函数

```cpp
#include <iostream>
using namespace std;
// 带有两个参数的模板函数：
template<class X,class R> apply(R (*fun) (X),X arg) {
  return fun(arg);
}
// 普通函数（有一个 double 类型的参数并返回 double 类型的结果）：
double f(double x) {
  return x*(1-x);
}
// 普通函数（有一个 int 类型的参数并返回 int 类型的结果）：
int factorial(int n) {
  if(n==0) {
    return 1;
  } else {
    return n*factorial(n-1);
  }
}
// 普通函数（有一个 int 类型的参数并返回 char 类型的结果）：
char symb(int n) {
  return 'A'+n;
}
// 程序的主函数：
int main() {
    cout << apply(f, 0.5) << endl;
    cout << apply(factorial, 5) << endl;
    cout << apply(symb, 3) << endl;
    return 0;
}
```

```cpp
template<> void show<MyClass>(MyClass obj) {
    obj.show();
}
// 程序的主函数:
int main() {
    MyClass obj(300);
    // 调用模板函数:
    show('A');
    show(100.0);
    show(200);
    show(obj);
    return 0;
}
```

程序的输出如下：

| 函数参数: A |

| 函数参数: 100 |

| 整数参数: 200 |

| 类 MyClass 类的对象: 300 |

在程序中，我们描述了一个带有一个参数的模板函数 `show()`，该参数的类型通过模板参数定义。该函数打印其参数的值。同时，我们还创建了该函数的两个显式特化。这些特化版本实现了当参数为整数（类型为`int`的值）以及当参数为 `MyClass` 类对象的情况。`MyClass` 类具有字段 `number` 和方法 `show()`，该方法会打印该字段。针对参数为 `MyClass` 类对象的函数 `show()` 显式特化，提供了从对象调用 `show()` 方法的功能。

## 第7章 模板函数与类

要描述模板函数的显式特化，我们从 `template` 关键字开始，后跟空尖括号 `<>`。紧接着是一个普通的函数描述。唯一的例外是，我们必须将我们要实现显式特化的类型标识符放在函数名之后，并在尖括号内。

## 模板类

与模板函数类似，我们可以创建模板类。在模板类中，可以使用参数作为类型标识符。

> **理论** 模板类的描述以 `template` 关键字开始，后跟一组用于模板类型的参数列表（每个参数前都跟有 `class` 关键字），并括在尖括号中。后面是类的具体描述，在其中我们可以使用这些模板类型参数。

当我们基于模板类创建对象时，在类名之后，我们在尖括号中放入代表模板参数的类型标识符。

列表 7.6 包含一个示例，在其中我们创建了一个模板类并在程序中使用它。

```cpp
Listing 7.6. 一个模板类
#include <iostream>
#include <string>

using namespace std;
// 模板类:
template<class A,class B> class MyClass{
public:
    // 类的字段:
    A first;
    B second;
    // 类的构造函数:
```

```cpp
MyClass(A f,B s) {
    first=f;
    second=s;
}
// 方法打印字段:
void show() {
    cout<<"The first field: "<<first<<endl;
    cout<<"The second field: "<<second<<endl;
}

// 程序的主函数:
int main() {
    // 基于模板类创建对象:
    MyClass<int,char> objA(100, 'A');
    MyClass<string,double> objB("text",10.5);
    MyClass<char*,string> objC((char*)"first","second");
    MyClass<int,int> objD(1,2);

    // 检查对象的字段:
    objA.show();
    objB.show();
    objC.show();
    objD.show();
    return 0;
}
```

程序的输出如下：

| 程序的输出（位于列表 7.6） |

| 第一个字段: 100 |

| 第二个字段: A |

| 第一个字段: text |

```text
The second field: 10.5
The first field: first
The second field: second
The first field: 1
The second field: 2
```

模板类的描述从 `template` 关键字开始。表达式 `<class A, class B>` 表示参数 A 和 B 代表类型标识符。接下来是 `MyClass` 的具体描述。也就是说，我们在类中声明了类型为 `A` 的字段 `first` 和类型为 `B` 的字段 `second`。替换 A 和 B 的类型在我们创建 `MyClass` 对象时定义。在类中，我们还描述了带有两个参数的构造函数（第一个类型为 `A`，第二个类型为 `B`），它决定了 `first` 和 `second` 字段的值。`show()` 方法打印这些字段。

在程序的主函数中，我们创建了几个对象。为了实现这一点，我们使用了语句 `MyClass<int,char> objA(100, 'A')`、`MyClass<string,double> objB("text",10.5)`、`MyClass<char*,string> objC((char*)"first","second")` 和 `MyClass<int,int> objD(1,2)`。在每个语句中，类名之后我们在尖括号中放入用于替代模板参数的类型标识符。例如，创建对象 `objA` 的表达式 `<int, char>` 表示使用 `int` 标识符代替参数 `A`，使用 `char` 标识符代替参数 `B`。在语句 `MyClass<string,double> objB("text",10.5)` 中，类型 `string` 用于第一个参数，相应地我们将字符串字面量 `"text"` 作为第一个参数传递给构造函数。众所周知，字符串字面量实现为字符数组，即类型 `char*`。尽管如此，由于自动转换，字面量被转换为 `string` 类型而无需直接干预。但如果我们使用类型 `char*` 来定义“string”类型，就必须从 `char*` 进行显式转换。语句 `MyClass<char*,string> objC((char*)"first","second")` 就是这种情况的示例。

## 细节

| 在语句 `MyClass<char*,string> objC((char*)"first","second")` 中，构造函数的第一个参数是字符串字面量。它作为 `char` 类型指针 (`const char*`) 传递给构造函数。要从 `char*` 转换，我们必须在相应的字符串字面量之前使用 `(char*)`。此外，两个模板参数可以是相同的。语句 `MyClass<int,int> objD(1,2)` 提供了一个例子。这里 A 和 B 都代表类型 `int`。 |

> 注意 为了使用 `string` 类，我们在程序中包含了 `<string>` 头文件。我们为每个对象调用 `show()` 方法来检查其字段。

## 模板类的显式特化

与模板函数一样，我们定义模板类的显式特化。让我们考虑列表 7.7 中的示例。

### 列表 7.7. 模板类的显式特化
