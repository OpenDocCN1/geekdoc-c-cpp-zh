
第9行的语句 `one = a;` 执行后，变量如图6-11所示。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_422_0.png)

**图 6-11** 第9行语句执行后变量的值

第10行的语句 `a++;` 执行后，变量如图6-12所示。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_422_1.png)

**图 6-12** 第10行语句执行后变量的值

第11行的语句 `b = b * 2;` 执行后，变量如图6-13所示。（注意，变量 b 改变了 num2 的值。）

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_422_2.png)

**图 6-13** 第11行语句执行后变量的值

第12行的语句 `v = 'B'` 执行后，变量如图6-14所示。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_423_0.png)

**图 6-14** 第12行语句执行后变量的值

第13行的语句产生以下输出：

```text
Line 13: Inside funOne: a = 11, b = 30, v = B, and one = 10
```

第13行的语句执行后，控制返回到第6行，为函数 funOne 的变量分配的内存被释放。图6-15显示了函数 main 的变量值。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_423_1.png)

**图 6-15** 控制返回到第6行时变量的值

第6行产生以下输出：

```text
Line 6: After funOne: num1 = 10, num2 = 30, and ch = A
```

第7行的语句是对函数 funTwo 的函数调用。现在 funTwo 有三个参数：x、y 和 w。此外，x 和 w 是引用参数，y 是值参数。因此，x 接收其对应实参的地址，即 num2；w 接收其对应实参的地址，即 ch。变量 y 将值 25 接收到其内存单元中。图6-16显示了第14行语句执行前的值。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_424_0.png)

**图 6-16** 第14行语句执行前变量的值

第14行的语句 `x++` 执行后，变量如图6-17所示。（注意，变量 `x` 改变了 `num2` 的值。）

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_424_1.png)

**图 6-17** 第14行语句执行后变量的值

第15行的语句 `y = y * 2` 执行后，变量如图6-18所示。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_424_2.png)

**图 6-18** 第15行语句执行后变量的值

第16行的语句 `w = 'G'` 执行后，变量如图6-19所示。（注意，变量 `w` 改变了 `ch` 的值。）

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_425_0.png)

第17行产生以下输出：

```text
Line 17: Inside funTwo: x = 31, y = 50, and w = G
```

第17行的语句执行后，控制转到第8行。为函数 funTwo 的变量分配的内存被释放。函数 main 的变量值如图6-20所示。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_425_1.png)

第8行的语句产生以下输出：

```text
Line 8: After funTwo: num1 = 10, num2 = 31, and ch = G
```

第8行的语句执行后，程序终止。

## 示例 6-14

此示例还展示了引用参数如何操作实参。

```cpp
//Example 6-14: Reference and value parameters.
//Program: Makes you think.

#include <iostream>

using namespace std;

void addFirst(int& first, int& second);
void doubleFirst(int one, int two);
void squareFirst(int& ref, int val);

int main()
{
    int num = 5;

    cout << "Line 1: Inside main: num = " << num
         << endl;                                  //Line 1

    addFirst(num, num);                             //Line 2
    cout << "Line 3: Inside main after addFirst:"
         << " num = " << num << endl;              //Line 3

    doubleFirst(num, num);                          //Line 4
    cout << "Line 5: Inside main after "
         << "doubleFirst: num = " << num << endl;  //Line 5

    squareFirst(num, num);                          //Line 6
    cout << "Line 7: Inside main after "
         << "squareFirst: num = " << num << endl;  //Line 7

    return 0;
}

void addFirst(int& first, int& second)
{
    cout << "Line 8: Inside addFirst:  first = "
         << first << ", second = " << second << endl; //Line 8

    first = first + 2;                              //Line 9

    cout << "Line 10: Inside addFirst:  first = "
         << first << ", second = " << second << endl; //Line 10

    second = second * 2;                            //Line 11

    cout << "Line 12: Inside addFirst:  first = "
         << first << ", second = " << second << endl; //Line 12
}

void doubleFirst(int one, int two)
{
    cout << "Line 13: Inside doubleFirst:  one = "
         << one << ", two = " << two << endl;      //Line 13

    one = one * 2;                                  //Line 14

    cout << "Line 15: Inside doubleFirst: one = "
         << one << ", two = " << two << endl;      //Line 15

    two = two + 2;                                  //Line 16

    cout << "Line 17: Inside doubleFirst: one = "
         << one << ", two = " << two << endl;          //Line 17
}

void squareFirst(int& ref, int val)
{
    cout << "Line 18: Inside squareFirst: ref = "
         << ref << ", val = " << val << endl;       //Line 18

    ref = ref * ref;                                 //Line 19

    cout << "Line 20: Inside squareFirst: ref = "
         << ref << ", val = " << val << endl;       //Line 20

    val = val + 2;                                   //Line 21

    cout << "Line 22: Inside squareFirst: ref = "
         << ref << ", val = " << val << endl;       //Line 22
}
```

### 示例运行：

```text
Line 1: Inside main:  num = 5
Line 8: Inside addFirst:  first = 5, second = 5
Line 10: Inside addFirst:  first = 7, second = 7
Line 12: Inside addFirst:  first = 14, second = 14
Line 3: Inside main after addFirst:  num = 14
Line 13: Inside doubleFirst: one = 14, two = 14
Line 15: Inside doubleFirst: one = 28, two = 14
Line 17: Inside doubleFirst: one = 28, two = 14
Line 5: Inside main after doubleFirst:  num = 14
Line 18: Inside squareFirst: ref = 14, val = 14
Line 20: Inside squareFirst: ref = 196, val = 14
Line 22: Inside squareFirst: ref = 196, val = 16
Line 7: Inside main after squareFirst:  num = 196
```

函数 addFirst 的两个参数都是引用参数，函数 doubleFirst 的两个参数都是值参数。函数 main 中的语句：

```cpp
addFirst(num, num);
```

（第2行）将 num 的引用传递给函数 addFirst 的两个形参 first 和 second，因为这两个形参对应的实参相同。也就是说，变量 first 和 second 引用同一内存位置，即 num。图6-21说明了这种情况。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_428_0.png)

**图 6-21** 函数 `addFirst` 的参数

first 对其值所做的任何更改都会立即改变 second 和 num 的值。类似地，second 对其值所做的任何更改都会立即改变 first 和 num 的值，因为这三个变量引用同一内存位置。（注意，num 已初始化为 5。）

函数 `doubleFirst` 的形参是值参数。因此，函数 `main` 中的语句：

```cpp
doubleFirst(num, num);
```

（第4行）将 `num` 的值复制到 one 和 two，因为这两个形参对应的实参相同。图6-22说明了这种情况。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_428_1.png)

**图 6-22** 函数 `doubleFirst` 的参数

因为 one 和 two 都是值参数，one 对其值所做的任何更改都不会影响 two 和 num 的值。类似地，two 对其值所做的任何更改都不会影响 one 和 num 的值。（注意，在函数 `doubleFirst` 执行之前，num 的值为 14。）

函数 `squareFirst` 的形参 `ref` 是引用参数，形参 `val` 是值参数。变量 `ref` 接收其对应实参的地址，即 `num`；变量 `val` 复制其对应实参的值，该实参也是 `num`。因此，`num` 和 `ref` 都引用同一内存位置，即 `num`。图6-23说明了这种情况。
