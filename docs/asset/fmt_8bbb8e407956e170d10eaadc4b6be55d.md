
程序的输出如下：

### 程序的输出（位于列表 4.1 中）
The argument: 0.523599
The cosine: 0.866025 vs. 0.866025
The sine: 0.5 vs. 0.5
The argument: 0.785398
The cosine: 0.707107 vs. 0.707107
The sine: 0.707107 vs. 0.707107
The argument: 1.0472
The cosine: 0.5 vs. 0.5
The sine: 0.866025 vs. 0.866025
The argument: 1.5708
The cosine: 3.26795e-07 vs. 3.26795e-07
The sine: 1 vs. 1

在程序中，我们创建了函数 `myFunction`（计算余弦）、`myFunction`（计算正弦）和 `show`（打印计算结果）。在程序的开头，这些函数只是进行了声明。它们的描述位于 `main()` 之后。

它在每次迭代中都会被加到和中。为了计算这个和，我们使用一个循环语句，循环控制变量 `k` 获取从 `0` 到 `n` 的值。在每次迭代中，语句 `s+=q` 会向和中添加一个新项，而语句 `q*(-1)*x*x/(2*k+1)/(2*k+2)` 则计算下一次迭代的项。计算完成后，变量 `s` 作为函数的返回返回。

## 注意事项

对于余弦函数，我们计算总和 $1 - \frac{x^2}{2!} - \frac{x^4}{4!} + \frac{x^6}{6!} - \dots + \frac{(-1)^n x^{2n}}{(2n)!} = q_0 + q_1 + q_2 + \dots + q_n$，其中 $q_k = \frac{(-1)^k x^{2k}}{(2k)!}$ 代表和中的项（在索引为 $k$ 的迭代中）。如果 $q_{k+1}$ 是下一次迭代的项，则 $q_{k+1} = q_k \cdot \frac{(-1)x^2}{(2k+1)(2k+2)}$。根据此，如果我们想计算下一次迭代，就应该将当前项乘以值 $\frac{(-1)x^2}{(2k+1)(2k+2)}$。我们在 `myCos()` 函数中实现了这一点。

对于正弦函数，我们计算总和 $x - \frac{x^3}{3!} + \frac{x^5}{5!} - \frac{x^7}{7!} + \dots + \frac{(-1)^n x^{2n+1}}{(2n+1)!} = q_0 + q_1 + q_2 + \dots + q_n$，其中 $q_k = \frac{(-1)^k x^{2k+1}}{(2k+1)!}$ 且 $q_{k+1} = q_k \cdot \frac{(-1)x^2}{(2k+2)(2k+3)}$。这就是为什么我们在 `mySin()` 函数中计算正弦时，我们将当前项乘以 $\frac{(-1)x^2}{(2k+2)(2k+3)}$，从而得到下一次迭代的项。

`mySin()` 函数计算正弦，它与计算余弦的 `myCos()` 函数类似。区别在于 `q` 的初始值是 `x`，我们使用语句 `q*(-1)*x*x/(2*k+2)/(2*k+3)` 来计算下一次迭代的项。

`show()` 函数原型中的 `void` 关键字意味着该函数不返回结果。该函数有一个类型为 `double` 的参数（记为 `x`）。`show()` 函数的参数决定了正弦和余弦函数的参数。

# 第章

## 函数

`show()` 函数打印参数，计算该参数的正弦和余弦，并打印结果。相应的，正弦和余弦是通过函数 `mySin()` 和 `myCos()` 计算的。我们还将计算结果与内置函数 `sin()` 和 `cos()` 的结果进行比较。

## 注意事项

要在程序中使用内置函数 `sin()` 和 `cos()`，我们需要包含 `<cmath>` 头文件。

在 `main()` 中，我们创建了 `double` 常量 `pi`。它的值是无理数 π $\approx$ 3.141592。然后我们使用参数 $\frac{\pi}{6}$、$\frac{\pi}{4}$ 和 $\frac{\pi}{2}$ 调用函数 `show()`。对于每个值，都会计算正弦和余弦并打印结果。正如我们所见，与借助内置函数计算出的值的吻合程度是完全可以接受的。

## 函数重载

在下一个程序，我们将计算银行持有者的收益。在这种情况下，我们需要知道银行账户的初始金额、年利率、存款期限（年）以及每年的计息次数。

## 细节

如果初始金额为 $m$，年利率为 $r$，存款期限（年）为 $t$，每年的计息次数为 $n$，则计算公式为 $A = m(1 + \frac{r}{n})^{nt}$。如果初始金额为 $m$……我们需要知道银行账户的初始金额、年利率、存款期限（年）以及每年的计息次数。

# 第 4 章 函数

列表 4.3 包含一个程序，我们在其中解决了之前定义的问题。然而，在这种情况下，我们创建了一个单一函数 `getMoney()`，它的两个参数都有默认值。

## 列表 4.3. 参数的默认值

```cpp
#include <iostream>
using namespace std;
// 带有默认值参数的函数：
double getMoney(double m,double r,int y=1,int n=1) {
    double s=m;
    double z=n*y;
    double q=r/n;
    for (int k=1;k<=z; k++) {
        s*=(1+q/100);
    }
    return s;
}
// 程序的主函数：
int main() {
    // 初始金额：
    double money=1000;
    // 年利率：
    double rate=5;
    cout<<"The initial amount: "<<money<<endl;
    cout<<"The annual interest rate: "<<rate<<"%\n";
    // 计算不同存款期限的
    // 最终金额：
    cout<<"The 1-year deposit: ";
    cout<<getMoney(money,rate)<<endl;
    cout<<"The 7-years deposit: ";
    cout<<getMoney(money,rate,7)<<endl;
    cout<<"The 7-years deposit\n";
    cout<<"the interest is charged 3 times per year: ";
    cout<<getMoney(money,rate,7,3)<<endl;
    return 0;
}
```

程序的输出与之前的情况相同：

```
The initial amount: 1000
The annual interest rate: 5%
The 1-year deposit: 1050
The 7-years deposit: 1407.1
The 7-years deposit
(the interest charge 3 times per year): 1414.98
```

当我们用三个参数调用 `getMoney()` 函数时，这等同于第四个参数等于 1（默认值）。如果我们用两个参数调用函数，那么意味着第三和第四个参数等于 1（这些参数的默认值）。

在函数的描述中，我们创建了三个局部变量。它们是 `s`，初始值为 `m`（初始金额）；`z`，值为 `n*y`（总计息次数）；`q`，值为 `r/n`（每期间的利率）。我们使用循环语句来计算结果。循环语句执行 `z` 次迭代，在每次迭代中，我们将 `s` 乘以 `(1+q/100)`。当循环语句终止时，变量 `s` 作为函数的返回返回。

这里我们使用了与上一个示例相同的计算算法，在上一个示例中我们创建了三个参数版本的函数。区别在于我们对有效利率和计息次数进行了一些“修正”。

> 注意事项
> 初看之下，我们有两个近乎相似的机制：函数重载和为参数定义默认值，后者更容易应用。这在原则上是正确的。另一方面，我们应该理解，函数重载是一项极具灵活性且高效的技术。我们不能用为参数定义默认值来取代它。

记住，同时使用函数重载和为参数定义默认值也是至关重要的。无论如何，我们必须以这种方式重载函数，以便根据调用语句确定被调用的函数版本和传递的参数。

## 使用递归

在函数的描述中，如果我们调用了同一个函数（通常带有不同的参数），则发生了递归。列表 4.4 包含一个使用递归的示例。我们解决了关于计算最终金额的相同问题。但在这里，为了简单起见，我们只考虑了一种计息方案：存款在给定的期限（年）内按固定利率存放，且每年计息一次。在程序中，我们描述了带有三个参数的 `getMoney()` 函数，并在函数描述中使用递归。现在我们将考虑下面的程序。

> 列表 4.4. 递归

```cpp
#include <iostream>
using namespace std;
// 带有递归的函数：
double getMoney(double m, double r, int y) {
  if (y == 0) {
    return m;
  } else {
    return (1 + r / 100) * getMoney(m, r, y - 1);
  }
}
int main() {
    double money = 1000;
    double rate = 5;
    cout << "The initial amount: " << money << endl;
    cout << "The annual interest rate: " << rate << "%\n";
    cout << "The 1-year deposit: ";
    cout << getMoney(money, rate, 1) << endl;
    cout << "The 7-years deposit: ";
    cout << getMoney(money, rate, 7) << endl;
    return 0;
}
```

程序的输出如下：

```
The initial amount: 1000
The annual interest rate: 5%
The 1-year deposit: 1050
The 7-years deposit: 1407.1
```

## 第4章 函数

```cpp
a=t;
for(int i=1;i<=20;i++){
    cout<<"-";
}
cout<<endl;
// 检查函数的参数：
cout<<"The first argument: "<<a<<endl;
cout<<"The second argument: "<<b<<endl;
cout<<"The swap () function is terminated"<<endl;
```
```cpp
// 程序的主函数：
int main(){
    // 要传递给函数的变量：
    char x='A',y='B';
    // 检查变量：
    cout<<"The first variable: "<<x<<endl;
    cout<<"The second variable: "<<y<<endl;
    // 调用函数：
    swap(x, y);
    // 检查变量：
    cout<<"The first variable: "<<x<<endl;
    cout<<"The second variable: "<<y<<endl;
    return 0;
}
```

我们可能期望在调用 `swap()` 函数后，传递给函数的变量会交换它们的值。然而，这里的程序的输出如下：

程序的输出（如 4.5 所示）

The first variable: A
The second variable: B
The swap() function is called

```text
The first argument: A
The second argument: B
----------------------
The first argument: B
The second argument: A
The swap() function is terminated
The first variable: A
The second variable: B
```

看起来参数在函数内部交换了它们的值。在调用 `swap()` 函数后，传递给函数的变量的值发生了变化。原因是参数是通过**值传递**传递给函数的。这意味着并不是将变量传递给函数，而是传递它们的副本。在函数结束后，变量的副本将从内存中删除。这种机制是默认使用的。这就是为什么当我们调用 `swap()` 函数时，所有的操作都是针对变量 `x` 和 `y` 的副本执行的。因此，交换的是副本的值。变量 `x` 和 `y` 的值仍然保持不变。

除了按值传递参数外，参数还可以通过**引用传递**传递。在这种情况下，变量本身（而不是它们的副本）被传递给函数。要通过引用传递变量，我们在函数定义的描述中在参数前加上 `&` 指令。在列表 4.6 中，我们创建了 `swap()` 函数，其参数是按引用传递的。与列表 4.5 中的程序相比，变化是极微的（大部分注释被删除了，并且在 `swap()` 函数的描述中，`&` 指令被加粗显示了）。

> ### 列表 4.6. <iostream>

```cpp
#include <iostream>
using namespace std;
// 按引用传递参数：
```
```cpp
void swap(char &a, char &b) {
cout<<"The swap () function is called"<<endl;
cout<<"The first argument: "<<a<<endl;
cout<<"The second argument: "<<b<<endl;
char t=b;
b=a;
a=t;
for(int i=1;i<=20;i++) {
cout<<"-";
}
cout<<endl;
cout<<"The first argument: "<<a<<endl;
cout<<"The second argument: "<<b<<endl;
cout<<"The swap() function is terminated"<<endl;
}
int main() {
char x='A',y='B';
cout<<"The first variable: "<<x<<endl;
cout<<"The second variable: "<<y<<endl;
swap(x,y);
cout<<"The first variable: "<<x<<endl;
cout<<"The second variable: "<<y<<endl;
return 0;
}
```

程序的输出如下所示：

| 程序的输出（如 4.6 所示） |
| :--- |
| The first variable: A |
| The second variable: B |
| The swap() function is called |
| The first argument: A |

```text
The second argument: B
-------------------
The first argument: B
The second argument: A
The swap() function is terminated
The first variable: B
The second variable: A
```

可以看到，变量在 `swap()` 函数后交换了它们的值。

## 将指针传递给函数

接下来我们将学习如何向函数传递指针。特别是，我们创建了另一个 4.7 版本。

```cpp
#include <iostream>
using namespace std;
// 参数为指针的：
void swap(char *a, char *b) {
cout<<"The swap () function is called"<<endl;
cout<<"The first argument: "<<a<<endl;
cout<<"The second argument: "<<b<<endl;
char t=*b;
*b=*a;
*a=t;
for(int i=1;i<=20;i++) {
cout<<"-";
}
cout<<endl;
cout<<"The first argument: "<<a<<endl;
cout<<"The second argument: "<<b<<endl;
cout<<"The swap() function is terminated"<<endl;
}
int main() {
char x='A',y='B';
cout<<"The first variable: "<<x<<endl;
```
