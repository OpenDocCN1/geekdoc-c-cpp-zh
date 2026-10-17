
```cpp
#include <iostream>
#include <string>
using namespace std;
// 结构体的描述：
struct MyMoney{
    // 结构体的字段：
    string name;
    double money;
    double rate;
    int time;
};
// 该函数根据结构体的
// 实例计算最终金额：
double getMoney(MyMoney str) {
    double s=str.money;
    for(int k=1;k<=str.time;k++){
        s=s*(1+str.rate/100);
    }
    return s;
}
// 该函数打印关于
// 结构体实例的信息：
void show(MyMoney str) {
    cout<<"The name: "<<str.name<<endl;
    cout<<"The initial amount: "<<str.money<<endl;
    cout<<"The annual rate: "<<str.rate<<endl;
    cout<<"The term (in years): "<<str.time<<endl;
    cout<<"The final amount: "<<getMoney(str)<<endl;
}
// 程序的主函数：
int main() {
    // 第一个结构体实例：
    MyMoney cat={"Tom the Cat",1000,8,5};
    // 第二个结构体实例：
    MyMoney mouse={"Jerry the Mouse",1200,7,4};
    // 打印关于
    // 结构体实例的信息：
    show(cat);
    show(mouse);
    return 0;
}
```

这里是程序的输出：

![](img/e64df7d2dc5c46ad731e195b8c5b7691_310_0.png)

```
The name: Tom the Cat
The initial amount: 1000
The annual rate: 8
The term (in years): 5
The final amount: 1469.33
The name: Jerry the Mouse
The initial amount: 1200
The annual rate: 7
The term (in years): 4
The final amount: 1572.96
```

在程序中，我们描述了结构体 `MyMoney`。这个结构体有几个字段。类型为 `string` 的字段用于存储账户持有者的姓名。`money` 和 `rate` 两个类型均为 `double` 的字段分别存储初始金额和年利率。整数字段 `time` 用于存储期限（以年计）。

函数 `getMoney()` 计算最终金额。它返回一个 `double` 类型的值，并有一个参数 `str`，它是结构体 `MyMoney` 的实例。

在函数中，我们声明了局部变量 `s`，初始值为 `str.money`。它是实例 `str` 的 `money` 字段的值。接下来，我们使用循环语句。实例 `str` 的 `time` 字段的值决定了迭代次数。每次迭代，语句 `s=s*(1+str.rate/100)` 都将变量 `s` 的当前值乘以 `(1+str.rate/100)`。计算完成后，函数返回变量 `s` 的值作为结果。

## 细节

- 我们应该考虑到，如果初始金额为 $m$，年利率为 $r$，期限为 $t$，那么最终金额为：

$$m(1 + \frac{r}{100})^t$$

函数 `show()` 不返回结果。它有一个参数 `str`，它是结构体 `MyMoney` 的实例。该函数打印实例 `str` 的 `name`、`money`、`rate` 和 `time` 字段。最终金额是通过 `getMoney()` 函数辅助计算的。

在程序的主函数中，我们创建并初始化了两个结构体 `MyMoney` 的实例 `cat` 和 `mouse`。为了实现这一点，我们使用了语句 `MyMoney cat={"Tom the Cat",1000,8,5};` 和 `MyMoney mouse={"Jerry the Mouse",1200,7,4};`。语句 `show(cat)` 和 `show(mouse)` 打印了这些实例的信息。

# 模板结构体

我们可以像模板类一样将模板参数传递给结构体。列表 8.2 包含了程序，我们在其中创建一个包含两个字段的模板结构体。我们通过模板参数定义字段的类型。程序中还描述了一个模板函数。该函数的参数是模板结构体的实例。

## 列表 8.2 模板结构体

```cpp
#include <iostream>
#include <string>
using namespace std;
// 模板结构体：
template<class A,class B> struct MyStruct{
    A first;
    B second;
};
// 模板函数处理
// 模板结构体的实例：
template<class A,class B> void
show(MyStruct<A,B> str) {
    cout<<"The first field: "<<str.first<<endl;
    cout<<"The second field: "<<str.second<<endl;
}
// 程序的主函数：
int main() {
    // 创建模板结构体的实例：
    MyStruct<int,char> strA={100,'A'};
    MyStruct<double,string> strB={2.5,"text"};
    // 调用模板函数：
    show(strA);
    show(strB);
    return 0;
}
```

程序的输出如下：

```
The first field: 100
The second field: A
The first field: 2.5
The second field: text
```

复数（Complex Numbers）

标准库 `<complex>` 包含了复数。使用复数时，我们需要包含 `<complex>` 头文件。复数类型 `complex<T>` 是模板类。我们可以通过普通方式对复数进行加、减、乘、除运算。

```cpp
cout<<"The fraction: ";
```

# 第8章 不同的程序 318

```cpp
cout<<A<<"*" <<conj (A)<<endl;
// 根据其模和参数
// 定义该数值：
cout<<"Defining the number: ";
cout<<polar (abs (A), arg (A))<<endl;
return 0;
```

这里是程序的输出：

| 和: (3,4) + (2,-1) = (5,3) | |

| 差: (3,4) - (2,-1) = (1,5) | |

| 乘积: (3,4) * (2,-1) = (10,5) | |

| 分数: (3,4) / (2,-1) = (0.4,2.2) | |

| 和: (3,4) + 2 = (5,4) | |

| 差: (3,4) - 2 = (1,4) | |

| 乘积: (3,4) * 2 = (6,8) | |

| 分数: (3,4) / 2 = (1.5,2) | |

| 和: 3 + (2,-1) = (5,-1) | |

| 差: 3 - (2,-1) = (1,1) | |

| 乘积: 3 * (2,-1) = (6,-3) | |

| 分数: 3 / (2,-1) = (1.2,0.6) | |

| 实部: Re(3,4) = 3 | |

| 虚部: Im(3,4) = 4 | |

| 模: abs(3,4) = 5 | |

| 幅角: arg(3,4) = 0.927295 | |

| 复共轭: (3,4)* = (3,-4) | |

| 定义的数值: (3,4) | |

我们在这里看到了什么？我们将 `complex` 类的一个对象识别为一个复数。通过这些对象，我们可以进行与对普通数相同的操作。也就是说，我们可以对它们进行加、减、乘、除。

更重要的是，这些表达式中的一个操作数可以是普通数。当我们借助输出运算符打印 `complex` 类的对象时，我们会得到一对被括在括号内的值。这些数字是复数的实部和虚部。

我们借助特殊函数来执行一些操作。例如，我们可以通过 `abs()` 函数计算数值的模。`arg()` 函数计算数值的幅角。要计算共轭数，我们使用 `conj()` 函数。`polar()` 函数根据模和幅角创建一个复数。例如，如果 `A` 实现了一个复数，那么表达式 `polar(abs(A),arg(A))` 将给出通过另一个对象实现的相同数值。

`real()` 和 `imag()` 方法（我们从实现复数的对象调用它们）分别返回复数的实部和虚部。

## 数值数组

标准类库中的模板类 `valarray` 实现数值数组。要使用该类，我们在程序中包含 `<valarray>` 头文件。接下来，我们考虑一个程序，在程序中，我们实现了 `valarray` 类来创建一个数值数组，并用斐波那契数填充它。在程序执行期间确定数组的大小是非常重要的。

> 注意：在这里和接下来，我们提到了数组，但指的是 `valarray` 类的对象，它的属性使其类似于数组。使用“数组”一术语既方便又直观清晰，但我们应该理解它确实是一个对象。

现在我们准备考虑列表 8.4 中的程序。

## 列表 8.4. 数值数组的容器

```cpp
#include <iostream>
#include <valarray>
using namespace std;
int main() {
    // 用于存储数组大小的变量
    int n;
    cout<<"数组的大小：";
    // 获取数组的大小：
    cin>>n;
    // 创建数值数组：
    valarray<int> fibs(n);
    // 前两个元素
    fibs[0]=1;
    fibs[1]=1;
    cout<<"数组的元素为：" << endl;
    // 填充数组
    for(int k=2;k<n;k++) {
        fibs[k]=fibs[k-1]+fibs[k-2];
        cout<<fibs[k];
    }
    cout<<endl;
    return 0;
}
```

列表 8.4 的输出可能如下（由用户输入的部分加粗）：

数组的大小：10

1 1 2 3 5 8 13 21 34 55 

```cpp
// 得到的多项式：
for(i=0;i<=power(); i++){
    tmp[i]+=a[i];
}
for(i=0;i<=pol.power(); i++){
    tmp[i]+=pol[i];
}
// 方法的结果：
return tmp;
}

// 用于将多项式
// 与数字相乘运算符函数：
Polygon operator*( Polygon pol,double r) {
    // 一个局部对象：
    Polygon tmp(pol.power());
    // 计算结果
    // 多项式的系数：
    for(int k=0;k<=pol.power();k++) {
        tmp[k]=pol[k]*r;
    }
    // 结果的结果：
    return tmp;
}
// 用于将数字
// 与多项式相乘运算符函数：
Polygon operator*(double r,Polygon pol) {
    // 多项式乘以数字：
    return pol*r;
}

// 用于计算两个多项式
// 差的运算符函数：
Polynomial operator-(Polynomial x, Polynomial y) {
  // 第二个多项式乘以 -1
  // 并加到第一个多项式：
  return x+(-1)*y;
}

// 用于从多项式计算
// 导数的模板函数：
Polynomial Diff(Polynomial pol) {
  // 一个局部对象：
  Polynomial tmp(pol.power()-1);
  // 计算结果
  // 多项式的系数：
  for(int k=0;k<=tmp.power();;k++) {
    tmp[k]=pol[k+1]*(k+1);
  }

  // 方法的结果：
  return tmp;
}

// 程序的主函数：
int main() {
  // 带有系数的数组：
  double A[]={1,2,-1,1};
  double B[]={-1,3,0,2,-1,1};
  // 多项式的参数：
  double x=2;
  // 用于保存计算
  // 结果的对象：
  Polynomial res;
  // 第一个多项式：
  Polynomial P(A,3);
  cout<<"The polynomial P:\t";
  // 第一个多项式的系数：
  P.getAll();
  cout<<"The value P("<<x<<") = ";
  // 第一个多项式在点上的值：
  cout<<P(x)<<endl;
  // 导数：
  res=Diff(P);
  cout<<"The polynomial P':\t";
  // 来自多项式的
  // 导数系数：
  res.getAll();
  cout<<"The value P'("<<x<<") = ";
  // 导数在点上的值：
  cout<<res(x)<<endl;
  // 第二个多项式：
  Polynom Q(B,5);
  cout<<"The polynomial Q:\t";
  // 第二个多项式的系数：
  Q.getAll();
  cout<<"The value Q("<<x<<") = ";
  // 第二个多项式在点上的值：
  cout<<Q(x)<<endl;
  // 多项式的乘积：
  res=P*Q;
  cout<<"The polynomial P*Q:\t";
  // 乘积的系数：
  res.getAll();
  cout<<"The value (P*Q)("<<x<<") = ";
  // 乘积在点上的值：
  cout<<res(x)<<endl;
  // 多项式的和：
  res=P+Q;
  cout<<"The polynomial P+Q:\t";
  // 结果的系数：
  res.getAll();
  cout<<"The value (P+Q)("<<x<<") = ";
  // 结果在点上的值：
  cout<<res(x)<<endl;
  // 多项式的差：
  res=Q-P;
  cout<<"The polynomial Q-P:\t";
  // 差的系数：
  res.getAll();
  cout<<"The value (Q-P)("<<x<<") = ";
  // 差在点上的值：
  cout<<res(x)<<endl;
  return 0;
}
```

以下是程序的输出：

程序的输出（见列表 8.5）

| 多项式 P: | 1 | 2 | -1 | 1 |

| :--- | :--- | :--- | :--- | :--- |

| 值 P(2) = 9 | | | | |

| 多项式 P' | 2 | -2 | 3 | | |

| 值 P'(2) = 10 | | | | |

| 多项式 Q: | -1 | 3 | 0 | 2 | -1 | 1 |

| 值 Q(2) = 37 | | | | | | | |

| 多项式 P*Q: | -1 | 1 | 7 | -2 | 6 | -3 | 5 | -2 | 1 |

| 值 (P*Q)(2) = 333 | | | | | | | | | | |

| 多项式 P+Q: | 0 | 5 | -1 | 3 | -1 | 1 |

| 值 (P+Q)(2) = 46 | | | | | | | |

| 多项式 Q-P: | -2 | 1 | 1 | -1 | -1 | 1 |

| 值 (Q-P)(2) = 28 | | | | | | |

## 第8 章

## 不同的程序

## 动态数组

标准库包含了 `vector` 类。该类的特征与动态数组的特征相似。然而，与动态数组相比，`vector` 类高效得多。

> 注意

使用 `vector` 类时，必须在程序中包含 `<vector>` 头文件。

## C++20 标准

除了 `vector` 类，为了存储数组，我们还可以使用 `array` 模板类。C++20 标准引入了 `to_array()` 函数，它可以将数组的对象转换为数组。

# 第 8 章 不同的程序

```cpp
cout<<"";
// 计算并打印元素：
for(int k=0;k<symbs.size();k++) {
    // 一个随机字符：
    symbs[k]='A'+rand()%(n+5);
    // 打印元素：
    cout<< "<<symbs[k]<<"";
}
cout<<endl;
return 0;
```

这里是该程序可能的输出（由于我们使用了随机字符，用户输入的数字已用**粗体**标记）：

- 程序的输出（见代码列表 8.6）

| 字符数量: 12 | |

| L | K | H | N | G | P | E | N | M | H | P | D |

尽管这段代码非常简单，但让我们来分析它。为了创建一个带有数组的节点，我们使用语句 `vector<char> symbs(n)`。对象 `symbs` 是基于模板类 `vector` 创建的，它包含一个含有 `n` 个 `char` 类型元素的数组。
