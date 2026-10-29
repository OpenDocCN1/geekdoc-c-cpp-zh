

# 静态类成员

每个类对象创建时，都会为其数据成员分配独立的内存块。然而，在某些情况下，让所有创建的对象共享同一个特定变量的内存位置会更方便。例如，在一个包含员工薪酬信息的类中，每个员工都适用相同的社会保险税率。显然，你可以将税率设为全局变量，但这种方法并不安全。作为全局变量，数据可能在程序的任何地方被修改，或与局部作用域中同名变量冲突，而且将其设为全局变量也违反了 C++ 的数据隐藏原则。

C++ 通过将类变量声明为 static 来处理这种情况。静态类变量为所有类对象共享同一存储空间；因此，它们充当类的全局变量，并为对象之间提供通信手段。C++ 要求在类声明部分声明静态类变量。这些变量的内存分配随后在类声明部分之外进行（即变量实际被创建）。例如，查看以下类声明，其中声明了一个名为 taxRate 的静态变量：

//class declaration section
class Employee
{
private:
    static double taxRate;
    int idNum;
public:
    Employee(int);  //constructor
    void display(); // accessor method
};
```

在类声明部分声明后，静态变量 taxRate 必须在声明部分之外进行定义（即创建）。以下语句可用于定义 taxRate：

```
double Employee::taxRate = 0.07;  // defines and initializes taxRate
```

![](img/e9bf940282dfb289356f077151cc69dd_493_0.png)

程序 10.7 的输出如下：

```
Employee number 11122 has a tax rate of 0.07
Employee number 11133 has a tax rate of 0.07
```

在对 taxRate 进行定义后，任何其他定义都会导致错误。因此，静态数据成员的实际定义仍由类创建者负责，如果省略此定义，编译器会报错。
图 10.5 说明了程序 10.7 中创建的静态数据成员和对象所产生的存储共享。

![](img/e9bf940282dfb289356f077151cc69dd_495_0.png)

## 图 10.5 共享静态数据成员 taxRate

除了静态数据成员之外，还可以创建静态成员方法。这些方法适用于整个类而不是特定的对象。因此，它们不是由对象调用的，并且只能访问类的静态数据成员和其他静态成员方法。程序 10.8 包含了一个静态成员方法的示例。请注意，在 main() 中对静态成员方法 dispRate() 的调用前面是其类名，而不是对象名。

## 程序 10.8

```
#include <iostream>
using namespace std;

// class declaration section
class Employee
{
    private:
        static double taxRate;
        int idNum;
public:
    Employee(int = 0);      // constructor
    void display();         // accessor method
    static void dispRate(); // static member method
};
// static member definition
double Employee::taxRate = 0.07;
// class implementation section
Employee::Employee(int num)
{
    idNum = num;
}
void Employee::display()
{
    cout << "Employee number " << idNum
         << " has a tax rate of " << taxRate << endl;
    return;
}
void Employee::dispRate()
{
    cout << "The static tax rate is " << taxRate << endl;
    return;
}
```

```
int main()
{
    Employee emp1(11122), emp2(11133);

    Employee::dispRate();  // call the static member methods
    emp1.display();
    emp2.display();

    return 0;
}
```

程序 10.8 产生以下输出：

```
The static tax rate is 0.07
Employee number 11122 has a tax rate of 0.07
Employee number 11133 has a tax rate of 0.07
```

```
double addimag(Complex &a, Complex &b)
{
    return(a.imag + b.imag);
}
```

```
int main()
{
    Complex a(3.2, 5.6), b(1.1, -8.4);
    double re, im;

    cout << "\n\nThe first complex number is ";
    a.display();
    cout << "\nThe second complex number is ";
    b.display();

    re = addreal(a,b);
    im = addimag(a,b);
    Complex c(re,im);  // create a new Complex object
    cout << "\n\nThe sum of these two complex numbers is ";
    c.display();

    return 0;
}
```

程序 10.9 产生以下输出：

```
The first complex number is 3.2+5.6i
The second complex number is 1.1-8.4i
The sum of these two complex numbers is 4.3-2.8i
```

在回顾程序 10.9 时，请注意以下四点：

- 因为友元不是类成员，所以它们不受声明时访问区段的影响——它们可以在声明区段的任何位置声明。程序 10.9 遵循的惯例是将所有友元声明放在类头之后立即声明。
- 关键字 friend（与关键字 static 类似）仅在类声明中使用，而不在实际的函数定义中使用。
- 因为友元函数旨在访问对象的私有变量，所以友元的至少一个参数应该是该类对象的引用，该类将它设为友元。
- 如程序 10.9 所示，是类授予方法友元身份，而不是相反。方法永远不能将自身设为友元，因为这样做违反了类提供的数据隐藏和访问概念。

## 练习 10.5

- 1. （修改）a. 重写程序 10.8，以包含一个名为 numemps 的整数静态变量。该变量应作为计数器使用，初始化为 0，并在每次声明新对象时由类构造函数递增。重写静态方法 dispRate() 以显示该计数器的值。
  b. 测试为练习 1a 编写的程序。让 main() 函数在每次创建 Employee 对象后调用 dispRate()。

- 2. （程序）a. 构造一个名为 Circle 的类，包含两个名为 xCenter 和 yCenter 的整数变量以及一个名为 radius 的双精度变量。此外，类还应包含一个名为 scaleFactor 的静态数据成员。xCenter 和 yCenter 值表示圆的中心点，radius 表示圆的实际半径，scaleFactor 表示用于将圆缩放以适应各种显示设备的缩放因子。
  b. 将为练习 2a 编写的类包含在一个可工作的 C++ 程序中。

- 3. （调试）a. 判断程序 10.9 中的以下三个语句
  re = addreal(a,b);
  im = addimag(a,b);
  Complex c(re,im); // create a new Complex object
  是否可以用以下单个语句替换：
  Complex c(addreal(a,b), addimag(a,b));
  b. 通过运行使用建议替换语句的程序 10.9 来验证你对练习 3a 的答案。

- 4. （修改）a. 重写为练习 2a 编写的程序，但包含一个友元函数，该函数将对象的半径乘以静态 scaleFactor，然后显示实际半径值和缩放后的值。
  b. 测试为练习 4a 编写的程序。

- 5. （修改）重写程序 10.9，使其仅有一个名为 addComplex() 的友元函数。该函数应接受两个 Complex 对象并返回一个 Complex 对象。返回对象的实部和虚部应为传递给 addComplex() 的两个对象的实部和虚部的和。

- 6. （程序）a. 构造一个名为 Coord 的类，包含两个名为 xval 和 yval 的双精度变量，用于存储点在直角坐标中的 x 和 y 值。类方法应包括构造函数和显示方法以及一个名为 convPol() 的友元函数。convPol() 函数应接受两个双精度数 r 和 theta，表示极坐标中的点，并将其转换为直角坐标。极坐标到直角坐标的转换使用以下公式：
  x = r cos(theta)
  y = r sin(theta)
  b. 将为练习 6a 编写的类包含在一个可工作的 C++ 程序中。

