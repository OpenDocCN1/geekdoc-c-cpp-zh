

Program 11.2 的 operator+() 函数以友元函数的形式编写如下：

```
Date operator+(Date& op1, int days)
{
    Date temp;  // a temporary Date to store the result

    temp.day = op1.day + days;  // add the days
    temp.month = op1.month;
    temp.year = op1.year;
    while (temp.day > 30)  // adjust the months
    {
        temp.month++;
        temp.day -= 30;
    }
    while (temp.month > 12)  // adjust the years
    {
        temp.year++;
        temp.month -= 12;
    }
    return temp;  // the values in temp are returned
}
```

该版本与成员函数版本之间的唯一区别在于友元版本中显式使用了名为 op1 的 Date 参数（名称是任意选择的）。因此，在友元函数的主体中，前三个赋值语句引用 op1 的数据成员为 op1.day、op1.month 和 op1.year，而成员函数则直接将其参数引用为 day、month 和 year。

在确定将二元运算符重载为友元运算符函数还是成员运算符函数时，请遵循以下准则：对于不修改其任一操作数的二元函数（如 ==、+、- 等），友元函数更为合适；对于修改操作数的二元函数（如 =、+= 和 -= 等），成员函数更为合适。

## EXERCISES 11.1

- 1. (Practice) 在你的计算机上输入并运行 Program 11.1。
- 2. (Program) a. 定义一个名为 operator>() 的大于关系运算符函数，可与 Program 11.1 中声明的 Date 类一起使用。
  b. 定义一个名为 operator<() 的小于关系运算符函数，可与 Program 11.1 中声明的 Date 类一起使用。
  c. 将练习 2a 和 2b 中编写的运算符函数包含在一个可工作的 C++ 程序中。

## 3. (Debug) a. 判断以下加法运算符函数是否与 Program 11.2 中的函数产生相同的结果：

```
Date Date::operator+(int days)   // return a Date object
{
    Date temp;

    temp.day = day + days;      // add the days in
    temp.month = month + int(day/30);      // determine total months
    temp.day = temp.day % 30;      // determine actual day
    temp.year = year + int(temp.month/12);  // determine total years
    temp.month = temp.month % 12;      // determine actual month
    return temp;
}
```

b. 通过将该函数包含在一个可工作的 C++ 程序中来验证对练习 3a 的回答。

## 4. (Program) a. 构造一个名为 Cartesian 的类，包含两个双精度数据成员 x 和 y，用于存储矩形坐标中点的 x 值和 y 值。成员函数应包括一个将对象的 x 和 y 值初始化为 0 的构造函数，以及用于输入和显示对象的 x 和 y 值的函数。此外，还包括一个在两个 Cartesian 对象之间执行逐成员赋值的赋值函数。

b. 将练习 4a 中编写的类包含在一个可工作的 C++ 程序中，该程序创建并显示两个 Cartesian 对象的值；第二个对象被赋予第一个对象的值。

## 5. (Program) a. 构造一个名为 Time 的类，包含三个整数数据成员 hrs、mins 和 secs，用于存储小时、分钟和秒。成员函数应包括一个为每个数据成员提供默认值 0 的构造函数、打印对象数据值的显示函数，以及在两个 Time 对象之间执行逐成员赋值的赋值运算符。

b. 将练习 5a 中开发的 Time 类包含在一个可工作的 C++ 程序中，该程序创建并显示两个 Time 对象；第二个对象被赋予第一个对象的值。

## 6. (Program) a. 构造一个名为 Complex 的类，包含两个双精度数据成员 real 和 imag，用于存储复数的实部和虚部。成员函数应包括一个为每个数据成员提供默认值 0 的构造函数、打印对象数据值的显示函数，以及在两个 Complex 对象之间执行逐成员赋值的赋值运算符。

b. 将练习 7a 中编写的类包含在一个可工作的 C++ 程序中，该程序创建并显示两个 Car 对象；第二个对象被赋予第一个对象的值。

## 8. (Program) a. 创建一个名为 String 的类，并包含一个连接两个字符串的加法运算符函数。该函数应返回一个字符串。

b. 将练习 8a 中编写的重载运算符包含在一个可工作的 C++ 程序中。

## 9. (Program) a. 定义一个可与 Program 11.1 中声明的 Date 类一起使用的减法运算符函数。减法应接受一个 long 整数参数，表示从对象的日期中减去的天数，并返回一个 Date。在进行减法时，假设所有月份均包含 30 天，所有年份均包含 360 天。此外，如果需要，应进行月末调整，将任何 resulting day 为 31 的情况转换为 day 为 30，除非月份为二月。如果 resulting month 为二月且 day 为 29、30 或 31，则应将其更改为 28。

b. 定义另一个名为 operator-() 的减法运算符函数，可与 Program 11.1 中定义的 Date 类一起使用。减法应产生一个 long 整数，表示两个日期之间的天数差。在计算天数差时，使用金融假设，即所有月份有 30 天，所有年份有 360 天。

c. 将练习 9a 和 9b 中编写的重载运算符包含在一个可工作的 C++ 程序中。

## 10. (Modify) a. 重写 Program 11.2 中的加法运算符函数，以考虑每个月的实际天数，省略闰年。 （注意：此函数需要一个数组来存储每个月的天数。）

b. 通过将其包含在一个可工作的 C++ 程序中来验证练习 10a 中编写的运算符函数的运行情况。

## 11. (Program) a. 构造一个名为 Fractions 的类，包含两个整数数据成员 num 和 denom，用于存储形如 num/denom 的分数的分子和分母。你的类应包括一个将 num 和 denom 初始化为 1 的默认构造函数，以及用于加、减、乘、除两个分数的四个运算符函数，如下所示：
Addition: a/b + c/d = (a * d + b * c) / (b * d)
Subtraction: a/b - c/d = (a * d - b * c) / (b * d)
Multiplication: a/b * c/d = (a* c) / (b * d)
Division: (a/b) / (c/d) = (a * d) / (b * c)
你的类应具有用于输入和显示分数的输入和输出函数。

b. 将练习 11a 中编写的类包含在一个可用于测试类的每个成员方法的 C++ 程序中。

## 12. (Modify) a. 将 Program 11.1 中的比较运算符函数重写为友元函数。

b. 通过将其包含在一个可工作的 C++ 程序中来验证练习 12a 中编写的友元运算符函数的运行情况。

方法在内存中对象所在的位置。在这种方式下，它使方法能够直接访问对象及其数据成员。例如，语句 `oldDate.showDate()` 将 oldDate 对象的地址传递给 showDate() 成员方法。

此时有两个问题如下：

- 如何将此地址传递给 `showDate()`？
- 此地址存储在哪里？

第一个问题的答案是，地址作为隐藏参数传递给被调用函数。因此，调用 `oldDate.showDate()` 将 `oldDate` 传递给 `showDate()`。请回顾第 8.1 节，将地址运算符 & 放在标识符前面表示“的地址”，因此表达式 `&oldDate` 应读作“oldDate 的地址”。因此，调用 `oldDate.showDate()` 相当于 `showDate(&oldDate)`。尽管此调用无效，因为它违反了调用成员方法的语法规则，但它清楚地说明了一个地址被传递了。那么问题是如何保存传递的地址并由 `showDate()` 访问？

它以与任何传递的地址必须被保存相同的方式保存——通过使用指针。这个特殊指针在方法定义时作为每个非静态类方法的隐藏参数自动创建。该特殊指针的名称是 this，接下来进行描述。

## The this Pointer

this 指针作为每个非静态类方法的隐藏参数自动添加。当方法被调用时，被调用对象的地址被传递给它并存储在方法的 this 指针中。因此，每个成员方法实际上接收一个额外的参数，即对象的地址。

虽然通常不需要这样做，但 this 指针中的地址可以在被调用方法中显式使用。例如，当 `showDate()` 由表达式 `oldDate.showDate()` 调用时，`showDate()` 中的 this 指针可用于通过以下语法访问 oldDate 对象中的任何数据成员：

```
(*this).month accesses oldDate’s month member.
(*this).day accesses oldDate’s day member.
(*this).year accesses oldDate’s year member.
```

这些关系如图 11.4 所示。如图所示，oldDate 对象的起始地址也是对象第一个数据成员的地址。除了使用点符号来定位正确的成员项外，它与你在第 8.4 节中看到的传递地址的技术相同。

