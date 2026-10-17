
由于参数是通过引用传递的，`Parameter` 不是 `argument` 的拷贝，而是后者的别名，就像列表 8.17 中的许多 `Ref` 一样。此外，接受引用作为参数的函数可以选择地使用引用参数返回返回值。参见列表 8.18 以了解函数如何使用引用而不是返回值。

# 列表 8.18 通过引用参数返回计算平方的函数

```cpp
0: #include <iostream>

1: using namespace std;

2:

3: void GetSquare(int& number)

4: {

    number *= number;

6: }

7:

8: int main()

9: {

10:    cout << "Enter a number you wish to square: ";

11:    int number = 0;

12:    cin >> number;

13:

14:    GetSquare(number);

15:    cout << "Square is: " << number << endl;

16:

17:    return 0;

18: }
```

# 输出 ▼

Enter a number you wish to square: 5
Square is: 25

# 分析 ▼

执行平方操作的函数位于第 3-6 行。注意它是如何通过引用参数接受待平方的数字并以相同方式返回结果的。如果你忘记将参数 `number` 标记为引用 `(&)`，结果将无法传递给调用函数 `main()`。

在这种情况下，发送待平方数字的变量也持有了结果。使用引用，结果在函数退出后在 `main()` 中可用。

#

# 在引用上使用 const

你可能需要不允许更改的引用。在声明引用时使用 `const` 是实现这一点的方法：

```cpp
int original = 30;

const int& constRef = original;

constRef = 40; // 不允许

int ref2 = constRef; // OK

const int& ref3 = constRef; // 不允许
```

# 通过引用传递参数

引用的主要优势之一是它们允许调用函数处理未复制的参数，从而显著提高性能。然而，由于调用函数直接在栈上操作，确保调用函数无法更改变量很重要。定义为 `const` 的引用可以帮助实现这一点，正如 8.19 所示。`const` 引用不能作为左值，因此对其进行任何赋值会导致编译失败。

# 列表 8.19 使用 const 引用确保调用函数无法修改传递的值

```cpp
0: #include <iostream>

1: using namespace std;

2:

3: void GetSquare(const int& number, int& result)

4: {

5:     result = number*number;

6: }

7:

8: int main()

9: {

10:    cout << "Enter a number you wish to square: ";

11:    int number = 0;

12:    cin >> number;

13:

14:    int square = 0;

15:    GetSquare(number, square);

16:    cout << number << " ^2 = " << square << endl;

17:

18:    return 0;

19: }
```

# 输出 ▼

Enter a number you wish to square: 27
27^2 = 729

# 分析 ▼

与列表 8.18 中发送待平方数字的变量也持有了结果相比，此程序使用了两个变量——一个发送待平方的数字，另一个用于持有结果。为了确保发送的值不能被修改，它被标记为 `const` 引用，如第 3 行所示。这自动使参数 `number` 成为输入参数——一个值不能被修改的参数。

作为实验，你可能会修改第 5 行使用列表 8.18 所示的逻辑返回平方：

`number *= number;`

你一定会遇到一个编译错误，告诉你 `const` 值无法被修改。因此，`const` 引用表示参数是输入参数并确保其值不能被修改。起初看起来这似乎微不足道，但在

在一个多程序环境中，由于编写第一个版本的人可能与改进该版本的人不是同一个人，使用 `const` 引用将有助于提高程序的质量。

## 总结

在本节中，你学习了指针和引用。你学习了如何使用指针访问和操作内存，以及它们是如何作为辅助动态内存分配的工具的。你学习了用于为元素分配内存的运算符 `new` 和 `delete`。你学习了它们的变体 `new[]` 和 `delete[]` 它们如何帮助你为数据数组分配内存。你接触了指针编程和动态内存分配中的陷阱，并发现释放动态分配的内存对于避免泄漏至关重要。引用是别名，在向函数传递参数时，它是使用指针的强大替代方案，因为引用被保证是有效的。你学习了在使用指针和引用时什么是“const 正确（const correctness）”，从今以后尽可能使用最严格的 `const` 级别来声明函数。

## 问答

- Q: 既然可以使用不需要担心释放内存的静态数组，为什么还要用动态分配内存呢？
- A: 静态数组的大小是固定的，如果你的应用程序需要更多内存，它将无法扩展；如果应用程序需要更少内存，它也不会进行优化。这正是动态内存分配发挥作用的地方。

两个指针：

```cpp
int* pointToIntAns = new int;

int* pCopy = pointToIntAns;
```

我难道不是调用 `delete` 来确保内存消失更好吗？

A: 那样做是错误的。你只允许对 `new` 返回的地址调用一次 `delete`。此外，理想情况下，在对任何一个指针执行 `delete` 之前，你有两个指针指向同一个地址，否则会使另一个指针失效。你的程序编写方式也不应该让你对所用指针的有效性产生任何不确定性。

- Q: 我应该什么时候使用 `new(nothrow)`？
- A: 如果你不想处理异常 `std::bad_alloc`，你可以使用运算符 `new` 的 `nothrow` 版本，它在请求的分配失败时返回 `NULL`。

## 我可以使用以下两种方法调用函数计算面积：

```cpp
void CalculateArea(const double* const ptrRadius, double* const ptrArea);

void CalculateArea(const double& radius, double& area);
```

## 我应该倾向于哪种变体？

- A: 后者使用引用的，因为引用不会失效，而指针可能会。此外，它也更简单。

## 我有一个指针：

```cpp
int number = 30;

const int* pointToAnInt = &number;
```

我理解由于 `const` 声明，我不能通过指针 `pointToAnInt` 修改 `number` 的值。我可以将 `pointToAnInt` 赋值给一个非 const 指针，然后使用它来操作整数 `number`set的值吗？

- A: 不，你不能改变指针的 const 正确性：

```cpp
int* aPointer = pointToAnInt; // 不能将指针赋值给 const
```

- Q: 我应该费心通过引用向函数传递值吗？
- A: 只要不怎么影响你的程序性能，你就不需要这样做。然而，如果你的函数参数接收的是非常重的对象（字节数大），按值传递将是非常昂贵的操作。使用引用会让你的函数调用高效得多。记住慷慨地使用 `const`，除非函数需要将结果存储在变量中。

## 这两个声明之间的区别是什么：

```cpp
int myNumbers[100];

int* myArray[100];
```

- A: `myNumbers` 是一个整数数组——也就是说 `myNumbers` 是一个指向存储 100 个整数的内存位置的指针，指向索引 0。它是以下代码的静态替代方案：

```cpp
int* myNumbers = new int [100]; // 动态分配的数组

// 使用 myNumbers

delete[] myNumbers;
```

另一方面，`myArray` 是指针数组，每个指针都可以指向一个整数或一个整数数组。

## 工作坊

工作坊提供了测试题帮助你巩固对涵盖内容的理解，并提供了使用所学知识的练习。在查看附录 E 中的答案之前，请回答测试和练习题，并确保你理解了答案。

## 测试

1. 为什么不能将 const 引用赋值给非 const 引用？
2. `new` 和 `delete` 是函数吗？
3. 指针变量包含的值的性质是什么？
4. 你使用哪个运算符访问指针所指向的数据？

## 练习

1. 执行以下语句时会显示什么：

```cpp
0: int number = 3;

1: int* pNum1 = &number;

2: *pNum1 = 20;

3: int* pNum2 = pNum1;

4: number *= 2;

5: cout << *pNum2;
```

2. 这三个重载函数之间有什么相似之处和不同之处：
`int DoSomething(int num1, int num2);`
`int DoSomething(int& num1, int& num2);`
`int DoSomething(int* pNum1, int* pNum2);`

3. 如何修改练习1中第1行中 `pNum1` 的声明，以便使第3 行的赋值无效？（提示：这与确保 `pNum1` 不能更改所指向的数据有关。）

4. 漏洞排除：这段代码有什么问题？

```cpp
#include <iostream>

using namespace std;

int main() {

    int* pointToIntAns = new int;

    int* pCopy = pointToIntAns;

    // 缺少了什么？

    return 0;

}
```

创建一个类型为 `Human` 的对象与创建另一个类型的实例相似，例如 `double`：

```cpp
double pi= 3.1415; // 一个 double 类型的变量

Human firstMan; //一个 Human 类的对象
```

或者，你也可以像创建另一个类型（例如 `int`）一样使用 `new` 动态创建一个 `Human` 类的实例：

```cpp
int* pointsToNum = new int; // 动态分配的整数

delete pointsToNum; // 使用后释放内存
```

```cpp
Human* firstWoman = new Human(); // 动态分配的 Human

delete firstWoman; // 释放内存
```

## 使用点运算符 (.) 访问成员

人类的一个例子是 Adam，男性，1970年出生于阿拉拉巴马州。实例 `firstMan` 是 `Human` 类的对象，是该类在现实中（即运行时）中的化身。

```cpp
Human firstMan; // Human 的一个实例
```

正如类声明所示，`firstMan` 拥有 `dateOfBirth` 等属性，可以使用点运算符 `()` 来访问：

```cpp
firstMan.dateOfBirth = "1970";
```

这是因为属性 `dateOfBirth` 属于 `Human` 类，正如类声明所示，它是类蓝图的一部分。该属性只有在对象实例化后才存在于现实中——即在运行时。点运算符 `(.`) 帮助你访问对象的属性。

对于 `IntroduceSelf()` 等方法也是如此：

```cpp
firstMan.IntroduceSelf();
```

如果你有一个指向 `Human` 类实例的指针 `firstWoman`，你可以使用指针运算符 (`--`) 来访问成员（如下一节介绍所示），或者使用间接运算符 `(*)` 配合点运算符来引用对象。

```cpp
Human* firstWoman = new Human();

(*firstWoman).IntroduceSelf();
```

## 使用指针运算符 (->) 访问成员

命名规范同样适用。类名和成员函数使用帕斯卡命名法（Pascal case）声明，例如 `IntroduceSelf()`。类成员属性使用驼峰命名法（camel case），例如 `dateOfBirth`。

当我们实例化一个类的对象时，我们声明一个类型为该类的变量。因此，我们使用驼峰命名法，这也是我们到目前为止一直用于变量名的方法，例如 `firstMan`。

注意

如果对象在空堆上使用 `new` 实例化，或者你有一个指向对象的指针，则你使用指针运算符 (`->`) 来访问成员属性和函数：

```cpp
Human* firstWoman = new Human();

firstWoman->dateOfBirth = "1970";

firstWoman->IntroduceSelf();

delete firstWoman;
```

列表 9.1 展示了一个带有 `public` 关键字的、可编译 `Human` 类。

- 列表 9.1 一个可编译的类 Human

```cpp
0: #include <iostream>

1: #include <string>

2: using namespace std;

3:

4: class Human

5: {

6: public:

7:     string name;

8:     int age;

9:

10: void IntroduceSelf()

11: {

12:     cout << "I am " + name << " and am " << \n;

13:     cout << age << " years:old" << endl;

14:

15: };

16:

17: int main()

18: {

19:     // 一个属性 name 为 "Adam" 的 Human 类对象

20:     Human firstMan;
```

# 第 9 节：类与对象

```cpp
21: firstMan.name = "Adam";

22: firstMan.age = 30;

23: 

24: // 一个属性 name 为 "Eve" 的 Human 类对象

25: Human firstWoman;

26: firstWoman.name = "Eve";

27: firstWoman.age = 28;

28: 

29: firstMan.IntroduceSelf();

30: firstWoman.IntroduceSelf();

31: }
```

## 输出 ▼

I am Adam and am 30 years old
I am Eve and am 28 years old

## 分析 ▼

第 4–15 行展示了一个基础 C++ 类 `Human`。注意 `Human` 类的结构以及该类如何在 `main()` 中被使用。

该类包含两个成员变量：第 7 行的 `string` 类型的变量 `name` 和第 8 行的 `int` 类型的变量 `age`。它还包含第 10–14 行的函数（也称为方法）`IntroduceSelf()`。`main()` 中的第 20 行和第 25 行实例化了两个 `Human` 类对象，分别命名为 `firstMan` 和 `firstWoman`。实例化后的行使用运算符设置了 `firstMan` 和 `firstWoman` 对象的成员变量，这在不久前已经解释过。注意第 29 行和第 30 行如何在输出的两个不同行中调用同一个函数 `IntroduceSelf()`。此程序演示了对象 `firstMan` 和 `firstWoman` 是独特的且个然不同的，它们是由 `Human` 类定义的抽象类型在现实世界中的代表。

你注意到到列表 9.1 中的 `public` 关键字了吗？是时候学习一些可以帮助你保护类中应该隐藏的属性的特征了。

## 关键字 public 和 private

信息至少可以分为两类：我们不在意公众公开的数据和私有数据。对于大多数人来说，性别是一个我们可能不介意分享的信息例子。然而，收入可能是一个私人问题。

C++ 允许你将类属性和方法建模为 `public` 或 `private`。因此，C++ 允许类设计者控制类数据属性的访问和操作方式。

在允许你将类设计为封装数据和操作这些数据的容器时，C++ 允许你通过 `private` 关键字决定哪些信息是外部世界无法访问的（即在类外部不可用）。同时，你也可以通过声明为 `public` 的方法对即使声明为 `private` 的信息进行受控访问。

回到 `Human::age` 为私有成员的例子，你发现许多人不喜欢透露自己的真实年龄。如果 `Human` 类需要返回一个比当前小两岁的年龄，可以通过一个 `public` 函数 `GetAge()` 轻松实现，该函数使用 `Human::age` 参数并减 2，结果如列表 9.2 所示。

## 列表 9.2 一个 Human 类模型，其中真实年龄对用户抽象化并报告较小的年龄

```cpp
0: #include <iostream>

1: using namespace std;

2:

3: class Human

4: {

5: private:

6: // 私有成员数据：

7: int age;

8:

9: public:

10: void setAge(int inputAge)

11: {

12: age = inputAge;

13: }

14:

15: // Human 对自己的年龄撒谎（如果超过 30 岁）

16: int getAge()

17: {
