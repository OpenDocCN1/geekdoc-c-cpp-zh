

```
point speed1(5, 7);
point speed2(1, 2);
point total;

total = speed1 + speed2;
cout << total.get_x() << endl;
cout << total.get_y() << endl;
```

事实上，我们可以通过重载 + 运算符来定义点的 + 的含义。重载的运算符有两个参数，即正在相加的两个点。函数返回这两个点的和，如下所示：

```
point operator + (const point& p1, const point& p2)
// Postcondition: The sum of p1 and p2 is returned.
{
   double x_sum, y_sum;

   // Compute the x and y of the sum.
   x_sum = p1.get_x() + p2.get_x();
   y_sum = p1.get_y() + p2.get_y();

   point sum(x_sum, y_sum);
   return sum;
}
```

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_104_0.png)

与二元比较运算符一样，二元算术运算符也可以定义为成员函数，而不是独立存在的函数。成员函数只有一个参数，即在类似 (p1 + p2) 的表达式中的右侧参数。左侧参数是激活成员函数的对象。我们的编程风格倾向于将二元运算符实现为非成员函数。

图 2.16 显示了 C++ 中最常被重载以执行算术运算的五个二元函数。

## 重载输出和输入运算符

标准 C++ 数据类型可以使用输出运算符 << 和输入运算符 >> 进行写入和读取。例如，我们可以读写一个整数：

```
int i;
cin >> i;
cout << i;
```

毫无疑问，你希望用你出色的新 point 类也做同样的事：

```
point p;
cin >> p; <--- reads the x and y coordinates
           of p from the standard input
cout << p; <--- writes the x and y coordinates
           of p to the standard output
```

你可以通过重载 << 和 >> 运算符为 point 类提供输入/输出功能。我们先从重载输出运算符开始，其神秘的原型如下所示：

```
ostream& operator <<(ostream& outs, const point& source);
```

让我们来揭开这个棘手原型的神秘面纱。该函数有两个参数：outs（是一个 ostream）和 source（是一个 point）。我们通过列出两个参数来使用该函数，如下所示：

```
cout << p; <--- The first argument, cout, is an ostream.
              The second argument, p, is a point.
```

如所示，cout 的数据类型是 ostream，意为“输出流”。ostream 类是 iostream 库设施的一部分。该设施还定义了 cout（控制台输出设备或“标准输出”），并为程序员定义其他输出流（例如连接到磁盘文件或打印机的输出流）提供了能力。无论如何，我们的意图是让 << 函数将名为 source 的点打印到名为 outs 的 ostream。我们现在可以写出大部分后条件：

```
ostream& operator <<(ostream& outs, const point& source);
// Postcondition: The x and y coordinates of source have been
// written to outs.
```

outs 参数是引用参数，意味着该函数可以更改输出流（通过向其中写入），并且更改会影响实际参数（例如标准输出流 cout）。source 参数是 const 引用参数，意味着该函数不会更改它正在写入的点。

还剩下最后一个谜团：该函数的返回类型是 ostream&：

```
ostream& operator <<(ostream& outs, const point& source);
```

大部分情况下，这个返回类型意味着函数返回一个 ostream。事实上，函数返回它刚刚写入的 ostream。& 符号还有额外含义（称为引用返回类型）。但我们要到第 6 章才会用到那个额外含义，因此只需知道输出和输入运算符都需要引用返回类型即可。

牢记这一点，我们现在可以写出完整的后条件：

```
ostream& operator <<(ostream& outs, const point& source);
// Postcondition: The x and y coordinates of source have been
// written to outs. The return value is the ostream outs.
```

函数返回 ostream 的原因是 C++ 将允许输出语句的“链式调用”，例如以下语句：

```
cout << "The points are " << p << " and " << q << endl;
```

此示例调用五个 << 函数，每个函数更改 ostream 并将结果传递给下一个函数调用。

point 的输出运算符的完整实现显示在图 2.17 的顶部。大部分工作由以下语句完成：

```
outs << source.get_x() << " " << source.get_y();
```

该语句使用普通的 << 运算符打印点的坐标，中间有一个空格字符。

## 图 2.17 点的输出和输入操作

## 函数实现

```
ostream& operator <<(ostream& outs, const point& source)
// Postcondition: The x and y coordinates of source have been
// written to outs. The return value is the ostream outs.
// Library facilities used: iostream
{
    outs << source.get_x() << " " << source.get_y();
    return outs;
}

istream& operator >>(istream& ins, point& target)
// Postcondition: The x and y coordinates of target have been
// read from ins. The return value is the istream ins.
// Library facilities used: iostream
// Friend of: point class
{
    ins >> target.x >> target.y;
    return ins;
}
```

point 的输入函数原型与输出函数类似，但它使用 istream（输入流）而不是 ostream，如下所示：

```
istream& operator >> (istream& ins, point& target);
// Postcondition: The x and y coordinates of target have been
// read from ins. The return value is the istream ins.
```

### operator >>

输入函数的实现显示在图 2.17 的底部。关键工作通过通常的 >> 运算符读取两个 double 数来完成，如下语句所示：

```
ins >> target.x >> target.y;
```

但等等！该语句将输入直接发送到 point 的私有成员变量 x 和 y。只有成员函数可以访问私有成员变量，而输入函数不是 point 的成员函数。这个问题有两种可能的解决方案：

- 1. 我们可以编写新的成员函数来设置点的坐标，并在输入函数的实现中使用这些成员函数。
- 2. 因为我们是 point 类的实现者，并且我们自己也在编写输入函数，所以可以授予输入函数访问 point 类私有成员的特殊权限。

第二种方法称为使用友元函数，我们现在来解释。

### 友元函数可以访问私有成员

## 友元函数

友元函数是一种不是成员函数，但仍能访问类对象私有成员的函数。要声明友元函数，将函数原型放在类定义中，并加上关键字 friend。

例如，要将 point 的输入函数声明为友元，我们必须在类定义中插入友元原型，如下所示：

```
class point
{
public:
  ...
  // FRIEND FUNCTIONS
  friend istream& operator >>(istream& ins, point& target);
private:
  ...
};
```

### 带有新友元的 point 类

一旦友元原型被放置在类定义中，函数体就可以访问其 point 参数的私有成员，如下所示：

```
istream& operator>>(istream& ins, point& target)
// Postcondition: The x and y coordinates of target have been
// read from ins. The return value is the istream ins.
// Library facilities used: iostream
// Friend of: point class
{
    ins >> target.x >> target.y;
    return ins;
}
```

请注意，友元函数不是成员函数，因此它不是由类的某个特定对象激活的。友元函数操作的所有信息都必须存在于其参数中。在函数体中直接写 x 或 y 是非法的；我们必须写 target.x 和 target.y。在我们的例子中，友元 operator >> 有一个 point 参数，友元函数可以访问的是该参数的私有成员变量。

友元可以授予给任何函数，而不仅仅是运算符函数。但友元应仅限于实现类的程序员编写的函数——毕竟，这个程序员是唯一真正了解私有成员的人。这样一来，新类的信息隐藏就能保持完好。

### 友元与信息隐藏

> ## 友元函数
> 
> 友元函数是一种不是成员函数，但仍需要访问其某些参数私有成员的函数。要声明友元函数，将函数原型放在类定义中，并加上关键字 friend。
> 
> 友元应仅限于实现类的程序员编写的函数。

## 何时使用友元函数

在实现类时，你通常会实现额外的函数来操作类的对象。如果函数需要访问类的私有成员，那么你首先应考虑通过成员函数提供访问。但是，如果出于其他原因成员函数不方便或不可接受，那么你可以授予函数友元，使其能够访问类的私有成员。

