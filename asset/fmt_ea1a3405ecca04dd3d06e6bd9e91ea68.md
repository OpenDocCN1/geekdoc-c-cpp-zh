
```
34     // 发现不匹配
35     return false;
36   }
37   low++;
38   high--;
39 }
40
41 return true;
42 }
```

```
Enter string: abba
abba is a palindrome
Enter string: abca
abca is not a palindrome
```

![](img/3b8bc24ba08ad32ac1a370eb095746a9_340_0.png)

程序在第 12 行声明字符串，在第 13 行从控制台读取，并调用`isPalindrome`检查是否为回文（第 15 行）。`isPalindrome`函数定义在第 23-41 行，字符串按引用传递。

## 10.5 对象数组

在第 7 章“一维数组”中，创建了基本类型的数组。你也可以声明对象数组。例如，以下语句声明了十个对象的数组：

`Circle circleArray[10];`

数组名称是`circleArray`，使用无参构造函数初始化数组中的每个元素。因此`circleArray[].getRadius()`返回 1。你也可以使用初始化列表来声明并初始化数组。例如：

`CircleArray[] = {Circle(3), Circle(4)};`

列表 10.4 给出了一个使用对象数组的示例。程序创建一个由十个对象组成的`circleArray`；设置每个对象的半径为 1、2、3……10，并显示数组中的面积。

### LISTING 10.4 TotalArea.cpp

```cpp
1 #include <iostream>
2 #include <iomanip>
3 #include "Circle2.h"
4 using namespace std;
5
6 // 计算面积
7 double sum(const Circle circleArray[], int size)
8 {
9 // 初始化 sum
10 double sum = 0;
11
12 // 将面积加到 sum
13 for (int i = 0; i < size; i++)
14 sum += circleArray[i].getArea();
15
16 return sum;
17 }
18
19 // 打印数组并显示它们的总面积
20 void printCircleArray(const Circle circleArray[], int size)
21 {
22 cout << setw(35) << left << "Radius" << setw(8) << "Area" << endl;
23 for (int i = 0; i < size; i++)
24 {
25 cout << setw(35) << left << circleArray[i].getRadius()
26 setw(8) << circleArray[i].getArea() << endl;
27 }
28 cout << " << endl;
29
31 // 计算并显示结果
32 cout << setw(35) << left << "The total area of circles is"
33 setw(8) << sum(circleArray, size) << endl;
34 }
35
36 int main()
37 {
38 const int SIZE = 10;
39 // 创建半径为 1 的圆对象
40 Circle circleArray[SIZE];
41
42 for (int i = 0; i < SIZE; i++)
43 {
44 circleArray[i].setRadius(i + 1);
45 }
46
47 printCircleArray(circleArray, SIZE);
48
49 return 0;
51 }
```

## 10.6 问题：改进扑牌解决方案

`circleArray[i].setRadius(i+1)`在`Circle`对象中设置了新新半径（第 45 行）。该数组被传递给`printCircleArray`函数，该函数显示所有圆的总面积半径。

圆面积之和使用`sum`函数计算（第 33 行），该函数接收`Circle`对象数组作为参数，并返回一个总面积的`double`值。

## 10.6 问题：改进扑牌解决方案

§7.4 展示了一个程序，它可以从一副 52 张的牌组中随机抽取四张牌。该程序使用两个函数`displayRank`和`displaySuit`来显示点数和花色。这两个函数可以通过在两个字符串数组中重新定义点数和花色来改进。

```cpp
const string suits[] = {"Clubs", "Diamonds", "Hearts", "Spades"};
const string ranks[] = {"Ace", "2", "3", "4", "5", "6", "7", "8", "9", "10", "Jack", "Queen", "King"};
```

列表 10.5 改进了 §7.4 中的程序。

### 列表 10.5 DeckOfCardsArrayOfStrings.cpp

```cpp
1 #include <iostream>
2 #include <string>
3 #include <ctime>
4
5 using namespace std;
6 const int NUMBER_OF_CARDS = 52;
7
8 // 洗牌数组中的元素
9 void shuffle(int list[], int size)
10 {
11 srand(time(0));
12 for (int i = 0; i < size; i++)
13 {
14 // 随机生成索引
15 int index = rand() % NUMBER_OF_CARDS;
16 int temp = list[i];
17 list[i] = list[index];
18 list[index] = temp;
19 }
20 }
21
22 int main()
23 {
24 int deck[NUMBER_OF_CARDS];
25 const string suits[] = {"Clubs", "Diamonds", "Hearts", "Spades"};
26 const string ranks[] = {"Ace", "2", "3", "4", "5", "6", "7", "8", "9", "10", "Jack", "Queen", "King"};
27
28 // 初始化牌
29 for (int i = 0; i < NUMBER_OF_CARDS; i++)
30 deck[i] = i;
31
32 // 洗牌
33 shuffle(deck, NUMBER_OF_CARDS);
34
35 // 显示前四张牌
36 for (int i = 0; i < 4; i++)
37 // 牌的点数
38 cout << ranks[deck[i] % 13] << " of"
39 // 牌的花色
40 << suits[deck[i] / 13] << endl;
41
42 return 0;
43 }
```

```cpp
40 << suits[deck[i] / 13] << endl;
41
42 return 0;
43 }
```

- 梅花 4
- 方片 A
- 红心 6
- 梅花 J

程序定义了一个`suits`数组用于四种花色（第 25 行），以及一个`ranks`数组用于每种花色中的 13 张牌（第 26–27 行）。这些数组中的每个元素都是`string`。考虑数组`suits`的声明：

```cpp
const string suits[] = {"Clubs", "Diamonds", "Hearts", "Spades"};
```

声明中的`suits[]`声明了一个数组。`string`部分声明数组中的每个元素都是`string`。放在数组中的四个值是 "Clubs""Diamonds"、"Hearts" 和 "Spades"。这是一个常量数组。

牌组在第 30-31 行被初始化为 0 到 31 的值。牌组值 0 代表梅花 A，1 代表梅花 2，13 代表方片 A，14 代表方片 2。

程序调用`shuffle`函数（第 34 行）来随机洗牌。牌组洗过后，`deck[i]`包含一个任意值。`deck[i]/13`是 0, 1, 2 或 3，决定了花色（第 40 行）。`deck[i] % 13`是 0 到 12 之间的值，决定了点数（第 39 行）。

## 10.7 实例和静态成员

到目前为止类类的数据字段被称为实例数据字段或实例变量。实例变量绑定到类的特定实例；它不会在同类的不同对象之间共享。例如，假设你使用列表 9.8 中的`Circle`类创建了以下对象：

```cpp
Circle circle1;
Circle circle2;
```

`circle1`中的半径与`circle2`中的半径是独立的，并存储在内存中。对`circle1`半径的修改不会影响`circle2`的半径，反之亦然。

如果你希望一个类的所有实例都共享数据，请使用静态变量，也称为类变量。静态变量将变量存储在公共的内存位置中。因此，如果一个对象改变了静态变量的值，同类的所有对象都会受到影响。C 语言支持静态函数以及静态变量。静态函数可以在创建类实例的情况下被调用。

在一个特定的圆上。因此，`radius`是`Circle`类的实例变量。由于`getArea`函数依赖于特定的圆，因此它是一个实例函数。由于`numberOfObjects`不依赖于任何特定实例，它应该被声明为`static`。

## 10.8 常量成员函数

你可以使用`const`关键字向编译器指定常量参数，说明该参数在函数中不应被更改。C++ 还允许你指定一个常量成员函数，告诉编译器该函数不会更改对象中任何数据字段的值。要这样做，请将`const`关键字放在函数头的末尾。例如，你可以像列表 10.9 所示重新定义列表 10.6 中的`Circle`类，头文件在列表 10.10 中实现。

## 列表 10.9 Circle4.h

```cpp
1 #ifndef CIRCLE_H
2 #define CIRCLE_H
3
4 class Circle
5 {
6 public:
7 Circle();
8 Circle(double) const;
9 double getArea() const;
10 double getRadius() const;
11 void setRadius(double);
12 static int getNumberOfObjects();
13
14 private:
15 double radius;
16 static int numberOfObjects;
17 };
18
19 #endif
```

## 列表 10.10 Circle4.cpp

```cpp
1 #include "Circle4.h"
2
3 int Circle::numberOfObjects = 0;
4
5 //构造一个圆对象
6 Circle::Circle()
7 {
8 radius = 1;
9 numberOfObjects++;
10 }
11
12 //构造一个圆对象
13 Circle::Circle(double newRadius)
14 {
15 radius = newRadius;
16 numberOfObjects++;
17 }
18
19 //返回此圆的面积
20 double Circle::getArea() const
21 {
22 return radius * radius * 3.14159;
23 }
24
25 // 返回此圆的半径
26 double Circle::getRadius() const
27 {
28 return radius;
29 }
31 // 设置新半径
32 void Circle::setRadius(double newRadius)
33 {
34 radius = (radius >= 0) ? newRadius : 0;
35 }
37 // 返回圆对象的数量
38 int Circle::getNumberOfObjects()
39 {
40 return numberOfObjects;
41 }
```

与常量参数一样，常量函数是为了防御性编程。如果你的函数错误地更改了函数中数据字段的值，编译器将报告编译错误。注意，你只能定义常量函数，而不能定义静态函数。

> 提示：你可以使用`const`修饰符来指定常量引用或常量成员函数。在适用的情况下，你应该一致地使用`const`修饰符。

## 10.9 面向对象的思维

![](img/3b8bc24ba08ad32ac1a370eb095746a9_350_0.png)

本书介绍了使用循环、函数和数组解决问题的基础编程技术。这些技术的研究为面向对象编程奠定了坚实的基础。类为构建可重用的软件提供了更大的活性和模块化。本节使用面向对象的方法来改进第 3 章介绍的问题解决方案。通过观察这些改进，你将了解过程化编程与面向对象编程之间的区别，并看到使用对象和类开发可重用代码的优势。

列表 3.3 `ComputeBMI.cpp`展示了一个计算体重指数的程序。该程序无法在其他程序重用。为了使代码可重用，定义一个计算体重指数的函数如下：

```cpp
double getBMI(double weight, double height)
```

该函数用于计算指定重量和高度的体重指数。然而，它有局限性。假设你需要将重量和身高与人的姓名关联。你可以声明变量来存储这些值，但这些值是紧耦合的。理想的方法是创建一个包含它们的对象。由于这些值与个体绑定，它们应该存储在实例字段中。你可以定义一个名为`BMI`的类，如图 10.11 所示。`BMI`类可以像列表 10.11 所示定义。这些数据字段的`get`函数在类中提供，但在 UML 图为了简洁而省略了。

| BMI |
| :--- |
| -name: string |
| -age: int |
| -weight: double |
| -height: double |
| +BMI(name: string, age: int, weight: double, height: double) | 人的姓名。 |
| +BMI(name: string, weight: double, height: double) | 人的年龄。 |
| +getBMI(): double | 人的重量（磅）。 |
| +getStatus(): string | 人的身高（英寸）。 |
| | 创建指定姓名、年龄和高度的 BMI 对象。 |
| | 返回 BMI。 |
| | 返回 BMI 状态（例如，正常、超重等）。 |

图 10.11 BMI 类封装信息

列表 10.11 BMI.h

```cpp
1 #ifndef BMI_H
2 #define BMI_H
3
4 #include <string>
5 using namespace std;
6
7 class BMI
8 {
9 public:
10 BMI(const string &newName, int age,
11 double newWeight, double newHeight);
12 BMI(const string &newName, double newWeight, double newHeight);
13 double getBMI() const;
14 string getStatus() const;
15 string getName() const;
16 int getAge() const;
17 double getWeight() const;
18 double getHeight() const;
19
20 private:
21 string name;
22 int age;
23 double weight;
24 double height;
25 };
26
27 #endif
```

> 提示：`string`参数`newName`使用`&newName`定义为引用传递。这通过防止编译器复制对象来提高性能。此外，引用定义为`const`以防止意外修改。你应该始终通过`const`引用传递对象。如果成员函数不更改数据字段，将其定义为常量函数。`BMI`类中的所有成员函数都是常量函数。列表 10.12 是该类的测试程序。

## 列表 10.12 BMIClass.cpp

```cpp
#include <iostream>
#include "BMI.h"
using namespace std;

int main()
{
    BMI bmi1("John Doe", 18, 70);
    cout << "The BMI for " << bmi1.getName() << " is " << bmi1.getBMI() << endl;
    BMI bmi2("Peter King", 25, 70);
    cout << "The BMI for " << bmi2.getName() << " is " << bmi2.getStatus();
    return 0;
}
```
