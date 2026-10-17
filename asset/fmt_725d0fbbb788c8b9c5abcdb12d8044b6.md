
## 31. 估计一口新气井含有 9000 吨在压力`p₀ = 900` psia 下的天然气。配气系统在排放压力`p* = 400` psia 处连接到该井。通过出口管道从井中排放的`Q`以吨/天计近似由方程`Q = α(p² − p*²)^β`给出，其中`α = 1.115 × 10⁻⁴`，`β = 0.8`，且`p` = 井内气体的初始压力，单位为 psia。还假设气体压力与排放量`Q`直接成比例，其由微分方程建模

```
dp/dt = -kQ
```

其中

```
k = 900 psia / 9000 tons = 0.1 psia / tons
```

合并这两个方程得到初值问题

```
dp/dt = -kα(p² - p*²)^β
p(0) = p₀
```

使用步长`Δt = 0.01`求解该初值问题并进行 10 步。

## 32. 下图显示了一个由绕在铁芯上的线圈、电阻、开关和电压源组成的电路：

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_219_0.png)

磁化曲线由方程给出

```
Ni = 1/2 Φ + 3/1000 Φ³
```

其中`N` = 线圈匝数，`i` = 电流（安培），`Φ` = 芯内磁通（千线）。基尔霍夫定律给出微分方程

`E = R i + L \frac{di}{dt} = R i + 10^{-5} \frac{d\Phi}{dt}`

其中`L` = 自感（亨利），`R` = 电阻（欧姆），`t` = 时间（秒）。假设`N = 100`且`R = 500`。则

`\frac{d\Phi}{dt} = E - 2.5\Phi' - 0.015\Phi^3, \quad \Phi(0) = 0`

其中`t`现在以毫秒为单位。 对于`E = 20 V`，求解该初值问题在区间 [0, 2] 中，使用步长`Δt = 0.01`。

## 33. 每年测量一次种群中的个体数量。设`P(t)`表示第`t`年的种群数量。设`α`表示出生率，并假设死亡率`β`与种群规模成正比，即`β = γ P(t)`，其中`γ`为常数。因此，种群的增长率由逻辑方程`P'(t) = α P(t) − γ [P(t)]²`给出。假设`P(0) = 50,000`，`α = 3 × 10⁻²`，且`γ = 1.5 × 10⁻⁷`。求解该初值问题，步长`Δt = 0.01`，以求出 5 年后的种群数量。

## 34.–38. 龙格-库塔法是求解一阶微分方程`y' = f(x, y)`且初始条件`y(x₀) = y₀`的一种流行且最精确的数值方法之一：

- 1. 选择`x`增量`Δx`。

- 2. 近似解`yₙ₊₁`在`xₙ₊₁ = x₀ + (n + 1)Δx`处，`n = 0, 1, 2, …`由

`yₙ₊₁ = yₙ + \frac{1}{6}(K₁ + 2K₂ + 2K₃ + K₄)`

给出，其中

`K₁ = Δx · f(xₙ, yₙ)`

`K₂ = Δx · f(xₙ + \frac{Δx}{2}, yₙ + \frac{K₁}{2})`

`K₃ = Δx · f(xₙ + \frac{Δx}{2}, yₙ + \frac{K₂}{2})`

`K₄ = Δx · f(xₙ + Δx, yₙ + K₃)`

编写程序实现龙格-库塔法并用其求解问题 29–33。

## 使用类

### 目录

- 7.1 入门示例：互联网地址 208
- 7.2 类简介 211
- 7.3 istream 和 ostream 类 218
- 7.4 string 类 228
- 7.5 C++ complex 类型 233
- 7.6 随机数模拟：屏蔽核反应堆 240
- 章节总结 245
- 自测 248
- 练习 251
- 编程问题 256

> 美国存在三个社会阶层：上中产阶级、中产阶级和下中产阶级。
> 
> 朱迪思·马丁（“礼仪小姐”）

> 程序是施加在计算机上的咒语，将输入转化为错误信息。
> 
> 匿名

> 对于每个复杂问题，都有一个清晰、简单且错误的答案。
> 
> H. L. MENCKEN

> 随机行善，不求回报，心安理得地知道有一天别人也可能为你做同样的事。
> 
> 戴安娜，威尔士王妃

THE WORD class IS often used to describe a group or category of objects that have a set of attributes in common. For example, the high school sports teams in one state are described as class A, class AA, class AAA, or class AAAA, depending on the number of students in the school. The usual classifications of secondary and college students are freshman, sophomore, junior, and senior. Metals, ceramics, polymers, semiconductors, and composites are classes of engineering materials, based on their chemical composition. The U.S. Navy uses Skipjack class, Thresher class, and Sturgeon class to characterize different kinds of submarines. Economists describe families as lower class, middle class, or upper class, based on their annual income. In these examples, class is used as a synonym for type because it provides a name for a group of related objects.

In Chapter 3, we studied the fundamental types provided in C++ to model basic objects such as numbers and characters: `int`, `unsigned`, `double`, `char`, `bool`, and variations of these such as `short`, `long`, and `float`. These types, however, cannot model more complex objects such as names of chemical elements, units of measurement, names and addresses of persons, and so on. None of the fundamental types, `char` type in particular, can adequately model these names because they consist of several characters and `char` values can only be single characters.

For situations like this, C++ provides libraries of standard classes to represent more complex objects. Also, programmers can build their own classes, thereby extending the C++ language. In this chapter, we will examine four standard C++ classes:

- the `istream` class to model input from a keyboard;
- the `ostream` class for modeling output to a screen;
- the `string` class for modeling sequences of characters;
- the `complex` class template to model complex numbers.

In the last section we will use

- a programmer-defined `RandomInt` class to generate random integers in a simulation program.

In Chapter 14 we will see how we can create our own classes.

### 7.1 INTRODUCTORY EXAMPLE: INTERNET ADDRESSES

IP (Internet Protocol) addresses are used to uniquely identify computers in the Internet; for example, titan.ksc.nasa.gov is the symbolic IP address of a site at the NASA Kennedy Space Center. Such an address is made up of four fields that represent specific parts of the Internet,

```
host.subdomain.subdomain.rootdomain
```

and is translated into a unique numeric IP address. This address is a 32-bit value, but it is usually represented in a dotted-decimal notation by separating the 32 bits into four 8-bit fields, expressing each field as a decimal integer, and separating the fields with a period; for example, at the time of this writing, 163.205.10.1 was the IP address for the above site at the NASA Kennedy Space Center. Each of the four parts is an 8-bit integer, so the entire address can be stored in 32 bits.

#### 7.1.1 Problem

A gateway is a device used to interconnect two different computer networks. Suppose that a gateway connects an engineering firm to the Internet and that the company’s network administrator needs to monitor connections through this gateway. Each time a connection is made, the IP address of the employee’s computer is transmitted to the network administrator, who analyzes the components that make up the address and records them.

#### 7.1.2 Object-Centered Design

##### 7.1.2.1 Behavior

The program will display on the screen a prompt for an IP address. The user will enter a string of characters from the keyboard, which the program will read. The program will then compute and output its four network/host information blocks on the screen along with descriptive text, or display an error message if the user did not enter a valid address.

##### 7.1.2.2 Objects

From the statement of the desired behavior, we can identify the following objects:

| Problem Objects | Type | Kind | Name | |
|---|---|---|---|---|
| Software Objects | | | | |
| screen | output device | variable | `cout` | |
| prompt | text string | constant | `none` | |
| IP address | text string | variable | `address` | |
| keyboard | input device | variable | `cin` | |
| network/host information blocks | text string | variable | `block1, block2, block3, block4` | |
| descriptive text error message | text string | constant | `none` | |

##### 7.1.2.3 Operations

Again, from the statement of the desired behavior, we can identify the following operations:

- i. Display a string on the screen.
- ii. Read a string from the keyboard.
- iii. Find each network/host information block and extract it from the string.
- iv. Display each information block on the screen.

##### 7.1.2.4 Algorithm

We now organize these operations into the following algorithm, which also shows how operation (iii) requires some refinement into simpler operations that are provided in C++.

+ 1. 输出提示输入 IP 地址到`cout`。
+ 2. 从`cin`输入`address`。
+ 3. 用`address`的适当子串填充`block1`，或在找不到时停止。
+ 4. 用`address`的适当子串填充`block2`，或在找不到时停止。
+ 5. 用`address`的适当子串填充`block3`，或在找不到时停止。
+ 6. 用`address`的适当子串填充`block4`，或在找不到时停止。
+ 7. 输出`block1`、`block2`、`block3`和`block4`到`cout`。

##### 7.1.2.5 编码与测试

Example 7.1 中的程序实现了该算法。它使用了 C++ 字符串类型，这是一个用于处理字符字符串的类。

###### Example 7.1 处理 IP 地址

```
/* This program finds the four network/host information blocks in an
IP address.

Input:  an IP address
Output: four network/host information blocks, or an error message
---------------------------------------------------------------*/

#include <iostream>      // cin, cout
#include <string>        // string class
#include <cassert>       // assert()
using namespace std;

int main()
{
    string address, block1, block2, block3, block4;

    cout << "Enter an IP address: ";
    cin >> address;

    // Search address to find first period -- start at position 0
    int dot1 = address.find(".", 0);
    assert(dot1 != string::npos);
    // Period found; set block1 = substring preceding it
    block1 = address.substr(0, dot1);

    // Search address for second period -- start at position dot1 + 1
    int dot2 = address.find(".", dot1 + 1);
```
