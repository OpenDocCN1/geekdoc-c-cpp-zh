
```cpp
    e--;
    d = c + a % c;

    cout << c << ", " << d << ", " << e;
    return 0;
}
```

- 3. 创建一个跟踪表，以确定该 C++ 程序在三次不同执行中每一步的变量值。然后，在 NetBeans IDE 中输入该程序，逐步执行，并确认结果。

  三次执行的输入值为：(i) 0.50，(ii) 3，以及 (iii) 15。

```cpp
#include <iostream>
using namespace std;
int main() {
    int a;
    double b, c;

    cin >> b;

    c = 5;
    c = c * b;
    a = 10 * c % 10;

    cout << a;
    return 0;
}
```

## “C++ 入门”中的复习题

回答以下问题。

- 1. 什么是算法？
- 2. 给出制作一杯咖啡的算法。
- 3. 算法的五个特性是什么？
- 4. 算法可以永远执行吗？
- 5. 什么是计算机程序？
- 6. 算法涉及哪三方？
- 7. 构成计算机程序的三个阶段是什么？
- 8. 计算机程序可以由两个阶段组成吗？
- 9. 什么是流程图？
- 10. 流程图可以原样输入计算机吗？
- 11. 流程图使用的基本符号有哪些？
- 12. “保留字”一词是什么意思？
- 13. 什么是结构化编程？
- 14. 结构化编程的三种基本控制结构是什么？
- 15. 使用流程图给出每种控制结构的示例。
- 16. 程序员可以在文本编辑器中编写 C++ 程序吗？
- 17. 什么是语法错误？给出一个示例。
- 18. 什么是逻辑错误？给出一个示例。
- 19. 拼错关键字、缺少标点字符或运算符使用不当会导致哪种类型的错误？
- 20. 程序员为什么应在代码中添加注释？
- 21. 程序员为什么应编写用户友好的程序？
- 22. 缩写 POLA 代表什么？
- 23. 什么是变量？
- 24. 在流程图中，左箭头的左侧可以存在多少个变量？
- 25. 变量的值存储在计算机的哪个部分？
- 26. 什么是常量？
- 27. 常量如何帮助程序员？
- 28. 计算机程序为什么应尽可能避免除法和乘法运算？
- 29. C++ 中变量和常量的四种基本类型是什么？
- 30. “声明变量”这个说法是什么意思？
- 31. 如何在 C++ 中声明变量？给出一个示例。
- 32. 如何在 C++ 中声明常量？给出一个示例。
- 33. 流程图中使用什么符号显示消息？
- 34. C++ 中使用什么特殊字符序列输出“换行”？
- 35. 流程图中使用什么符号让用户输入数据？
- 36. C++ 中使用哪个符号作为赋值运算符，它在流程图中如何表示？
- 37. C++ 支持哪些算术运算符？
- 38. 什么是取模运算符，它在流程图中通常如何表示？
- 39. 总结算术运算符的优先级规则。
- 40. C++ 支持哪些复合赋值运算符？
- 41. C++ 支持哪些自增/自减运算符？
- 42. C++ 支持哪些字符串运算符？
- 43. 什么是跟踪表？
- 44. 使用跟踪表有哪些好处？
- 45. 描述交换两个变量内容（数值或字母数字）所涉及的步骤。
- 46. 本书提出了两种交换两个变量值的方法。哪一种更好，为什么？
- 47. “调试”一词是什么意思？
- 48. 描述 NetBeans IDE 如何帮助你发现语法错误。
- 49. 描述 NetBeans IDE 如何帮助你发现逻辑错误。

## 第 3 部分：顺序控制结构

## 第 10 章：顺序控制结构简介

### 10.1　什么是顺序控制结构？

“顺序控制结构”是指逐行执行，即语句按照它们在程序中出现的相同顺序依次执行。例如，它们可能执行一系列读或写操作、算术运算，或对变量赋值。

顺序控制结构是你在第 4 章学到的三种基本控制结构中最简单的一种。下面的程序展示了按顺序执行的 C++ 语句示例。

```cpp
#include <iostream>
using namespace std;
int main() {
  double a, b;

  cout << "Enter a number: ";
  cin >> a;

  b = a * a;

  cout << "The square of " << a << " is " << b;
  return 0;
}
```

### 练习 10.1-1　*计算平行四边形的面积*

*编写一个 C++ 程序，计算并显示平行四边形的面积。*

### 解答

平行四边形的面积可以使用以下公式计算：

*面积 = 底 × 高*

在本练习中，用户输入*底*和*高*的值，程序计算并显示平行四边形的面积。该问题的解答如下所示。

```cpp
#include <iostream>
using namespace std;
int main() {
    double area, base, height;

    cout << "Enter the length of Base: ";
    cin >> base;
    cout << "Enter the length of Height: ";
    cin >> height;

    area = base * height;

    cout << "The area of the parallelogram is " << area;
    return 0;
}
```

### 练习 10.1-2　*计算圆的面积*

编写一个 C++ 程序，计算并显示圆的面积。

### 解答

圆的面积可以使用以下公式计算：

*面积 = π · 半径²*

π 的值是已知量，为 3.14159。因此，用户唯一需要输入的值是半径。该问题的解答如下所示。

**project_10_1_2a**

```cpp
#include <iostream>
using namespace std;
int main() {
    double area, radius;

    cout << "Enter the length of Radius: ";
    cin >> radius;

    area = 3.14159 * radius * radius;

    cout << "The area of the circle is " << area;
    return 0;
}
```

更好的方法是使用常量 PI。

**project_10_1_2b**

```cpp
#include <iostream>
using namespace std;
const double PI = 3.14159;

int main() {
    double area, radius;

    cout << "Enter the length of Radius: ";
    cin >> radius;
    area = PI * radius * radius;
    cout << "The area of the circle is " << area;
    return 0;
}
```

> **注意：** 请注意，常量 PI 声明在函数 main 之外。

### 练习 10.1-3　*计算燃油经济性*

在美国，汽车的燃油经济性以英里每加仑（MPG）来衡量。汽车的 MPG 可以使用以下公式计算：

$$\mathrm{MPG}=\frac{\text{miles driven}}{\text{gallons of gas used}}$$

编写一个 C++ 程序，提示用户输入其行驶的总英里数和使用的汽油加仑数。然后程序应计算并显示汽车的 MPG。

### 解答

这是一个相当简单的情况。用户输入其行驶的总英里数和使用的汽油加仑数，然后程序应计算并显示汽车的 MPG。

```cpp
#include <iostream>
using namespace std;
int main() {
    double gallons, miles_driven, mpg;

    cout << "Enter miles driven: ";
    cin >> miles_driven;
    cout << "Enter gallons of gas used: ";
    cin >> gallons;

    mpg = miles_driven / gallons;

    cout << "Your car's MPG is: " << mpg;
    return 0;
}
```

### 练习 10.1-4　*汽车在哪里？计算行驶距离*

一辆汽车从静止开始，在一条笔直的水平道路上以恒定加速度运动给定时间。编写一个 C++ 程序，提示用户输入

### 练习 10.1-5　*开尔文转华氏度*

编写一个 C++ 程序，将华氏度¹的温度值转换为其等效的开尔文度²。所需公式为

$1.8 \times Kelvin = Fahrenheit + 459.67$

### 解答

给出的公式不能原样用于程序中。在 C++ 这样的计算机语言中，不允许这样写

```cpp
1.8 * kelvin = fahrenheit + 459.67
```

> **记住！** 在 (=) 号左侧的位置上，只能存在一个变量。这个变量实际上是 RAM 中可存储值的区域。

该程序将华氏度转换为开尔文度。华氏度的值是由用户给出的已知值，而开尔文度的值是 C++ 程序应计算的值。因此，你需要求解开尔文。稍作推导后，公式变为

$Kelvin = \dfrac{Fahrenheit + 459.67}{1.8}$

对应的 C++ 程序如下所示。

**project_10_1_5**

```cpp
#include <iostream>
using namespace std;
int main(){
  double fahrenheit, kelvin;

  cout << "Enter a temperature in Fahrenheit: ";
  cin >> fahrenheit;

  kelvin = (fahrenheit + 459.67) / 1.8;

  cout << "The temperature in Kelvin is " << kelvin;
  return 0;
}
```

¹ 丹尼尔·加布里埃尔·华伦海特（Daniel Gabriel Fahrenheit，1686–1736）是一位德国物理学家、工程师和玻璃吹制工，最著名的是发明了酒精温度计和水银温度计，并制定了如今以他命名的温标。

² 威廉·汤姆森，第一代开尔文男爵（William Thomson, 1st Baron Kelvin，1824–1907），是一位出生于爱尔兰的英国数学物理学家和工程师。他因奠定绝对零度（开尔文温标）的基础而广为人知，因此一种温度计量单位以他的名字命名。他发现了热电中的汤姆孙效应，并帮助发展了热力学第二定律。

