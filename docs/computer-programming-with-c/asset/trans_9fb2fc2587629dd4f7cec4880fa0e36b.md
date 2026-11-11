

## 说明

语句

```cpp
s=p1.slope(p2);
```

使用对象 p1 调用成员函数 `slope()`，并将对象 p2 作为参数传递给该函数。成员函数 slope 创建一个名为 t 的另一个对象作为形参，因此可以通过对象 t 分别以 t.x 和 t.y 访问 p2 的成员 x 和 y。重要的是要理解，p2 和 t 是内存中的两个不同对象，但对象 p2 的成员值将与对象 t 的成员值相同，因为 p2 是实参，而 t 是形参。

你也可以不将 p2 和 t 创建为两个不同的对象，而是通过引用传递对象。通过将形参 t 创建为 Point 类型的引用而不是 Point 类型的对象，就可以按引用传递对象 p2，如下所示

```cpp
float slope(Point& t)
{
    float s;
    if(t.x-x!=0)
    {
        s=(float)(t.y-y)/(t.x-x);
        return s;
    }
    else
    {
        cout<<"Slope is undefined, printing a dummy value as 0"<<endl;
        return 0;
    }
}
```

> **t 是 Point 类型的引用变量，它将引用实际参数 p2**

`slope()` 函数中使用的其余逻辑与程序中给出的完全相同。当对象相对较大时，按引用传递对象总是比按值传递更好。这是因为按值调用（不同于按引用调用或按地址调用）会创建同一对象的两个不同副本，这可能在程序执行期间导致相当大的存储空间占用。

## 11.9 复数加法：一个示例

正如每个 Point 对象都通过指定其 x 值和 y 值来定义一样，每个复数也通过指定其实部和虚部来定义。因此，如代码所示，我们创建两个私有变量 real 和 img 作为 Complex 类的成员。

此外，我们需要在 Complex 类中提供如下列出的成员函数：

- `input()`：从用户处输入每个 Complex 对象的 real 和 img 值。
- `output()`：在计算机屏幕上打印每个 Complex 对象的 real 和 img 值。
- `add()`：执行两个 Complex 对象的加法并返回加法结果。

函数 `input()` 和 `output()` 将与前面示例中设计的函数类似。因此，我们从成员函数 `add()` 开始解释此示例。

如果 C1 和 C2 是 Complex 类的两个对象，并且我们需要将 C1 和 C2 的加法结果存储在另一个复数 C3 中，那么 C3 的实部值应通过将 C1 的实部与 C2 的实部相加得到，而 C3 的虚部值应通过将 C1 的虚部与 C2 的虚部相加得到。在没有数据隐藏的情况下，可以使用以下 C++ 语句实现：

```cpp
C3.real=C1.real+C2.real;
C3.img=C1.img+C2.img;
```

然而，我们知道成员 real 和 img 是 Complex 类的私有成员，因此我们必须在类内编写一个成员函数来执行 Complex 对象的加法。我们将此成员函数命名为 add()。

回想一下，类的成员函数总是使用该类的对象来调用。这意味着成员函数 add() 必须使用对象 C1 或对象 C2 来调用。如果我们使用对象 C1 调用成员函数 add()，那么对象 C1 的成员 real 和 img 的值可以在 add() 函数内直接访问，如图 11.26 所示。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_579_0.png)

如前所述，在 add() 函数内还需要复数对象 C2 的 real 和 img 值，以计算两个复数的加法结果。因此，我们应用与计算斜率示例中讨论的类似逻辑，并将 C2 作为参数传递给函数 add()。因此，我们如下调用函数 add()：

```cpp
C3= C1.add(C2);
```

成员函数 add() 由对象 C1 调用，并传递 C2 作为参数。这意味着 C1 的 real 和 img 值可以在 add() 函数内直接访问，而 C2 的 real 和 img 值必须分别通过对象 t 以 t.real 和 t.img 访问。这是因为 t 是对应于实际参数 C2 的形式参数，如图 11.27 所示。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_580_0.png)

此外，我们需要将加法结果存储在 Complex 对象 C3 中。然而，对象 C3 在 add() 函数内将不可访问，因为它的作用域仅限于 main()。因此，我们创建一个临时对象 res，用于在 add() 函数中存储两个复数的加法结果。对象 res 随后被返回给调用函数并初始化给对象 C3，如图 11.27 所示。因此，在 add() 完成执行后，加法结果将在 C3 中可用。

以下是执行复数加法的完整源代码：

```cpp
#include<iostream.h>
class Complex
{
private:
    int real;
    int img;
public:
    void input()
    {
        cin>>real>>img;
    }
    Complex add(Complex t)
    {
        Complex res;
        res.real=real+t.real;
        res.img=img + t.img;
        return res;
    }
    void output()
    {
        cout<<"Real part is "<<real<<"Img part is "<<img;
    }
};
void main()
{
    Complex C1,C2,C3;
    cout<<"Enter first Complex number"<<endl;
    C1.input();
    cout<<"Enter second Complex number"<<endl;
    C2.input();
    C3 = C1.add(C2);
    cout<<"Result Complex number is"<<endl;
    C3.output();
}
```

### 输出：

```
Enter first Complex number
10 5
Enter second Complex number
3 25
Result Complex number is
Real part is 13 Img part is 30
```

让我们从 main() 函数的第一行开始理解代码。

语句

```cpp
Complex C1,C2,C3;
```

创建了 Complex 类的三个对象。随后，我们通过在每个对象上调用 input() 函数，从用户处输入两个复数 C1 和 C2 的 real 和 img 值，如下所示：

```cpp
C1.input();
C2.input();
```

让我们假设用户为 Complex 对象 C1 和 C2 输入以下值，如表所示：

| Complex 类的对象 | 用户输入的数据（real, img） |
|---|---|
| C1 | (10, 5) |
| C2 | (3, 25) |

这意味着 Complex 对象 C1 和 C2 的状态如图 11.28 所示。

![](img/57c0d966bb33c67a5a188e6bf39e4e02_582_0.png)

下一条语句

```cpp
C3=C1.add(C2);
```

使用对象 C1 调用成员函数 `add()`，并传递 C2 作为参数。加法结果将在 `add()` 执行完成后返回并存储在对象 C3 中。现在，我们可以通过打印对象 C3 的成员 real 和 img 的值来输出复数加法的结果。这可以通过使用对象 C3 调用函数 `output()` 来完成，就像在 `main()` 函数的最后一行所做的那样。

## 11.10 笛卡尔坐标系中点的加法：一个示例

正如每个复数都有实部和虚部两部分一样，每个二维点都使用 x 和 y 坐标来定义。因此，我们可以像上一节执行复数加法那样，在笛卡尔坐标系中相加两个点。

下面给出执行 Point 对象加法的完整源代码：

```cpp
#include<iostream.h>
class Point
{
private:
int x;
int y;
public:
void input()
{
    cin>>x>>y;
}
void output()
{
    cout<<x<<"    "<<y<<endl;
}
Point add(Point t)
{
    Point res;
    res.x=x+t.x;
    res.y=y+t.y;
    return res;
}
};
void main()
{
    Point p1,p2,p3;
    cout<<"Enter first point"<<endl;
    p1.input();
    cout<<"Enter second point"<<endl;
    p2.input();
    p3 =p1.add(p2);
    cout<<"Resultant point is"<<endl;
    p3.output();
}
```

```
Enter first point
10 20
Enter second point
5 15
Resultant point is
15   35
```

该程序创建三个点对象 p1、p2 和 p3。对象 p1 和 p2 的 x 和 y 坐标值从用户处输入。

让我们假设用户为 Point 对象 p1 和 p2 输入以下值：

| Point 类的对象 | 用户输入的数据（x, y） |
|---|---|
| p1 | (10, 20) |
| p2 | (5, 15) |

语句

```cpp
p3 =p1.add(p2);
```

