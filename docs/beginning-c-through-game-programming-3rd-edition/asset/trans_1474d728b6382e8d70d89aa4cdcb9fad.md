

![](img/34f09be0ed6217c465debc4490197d4f_197_0.png)

## Figure 5.6

函数重载允许你使用相同的函数名对两种不同类型的数值进行三倍运算。

你可以在 Course Technology 网站 (www.courseptr.com/downloads) 上下载此程序的代码。该程序位于 Chapter 5 文件夹中；文件名是 triple.cpp。

```
// Triple
// Demonstrates function overloading

#include <iostream>
#include <string>

using namespace std;

int triple(int number);
string triple(string text);

int main()
{
```
```
cout << "Tripling 5: " << triple(5) << "\n\n";
cout << "Tripling 'gamer': " << triple("gamer");

    return 0;
}
```
```
int triple(int number)
{
    return (number * 3);
}
```
```
string triple(string text)
{
    return (text + text + text);
}
```

## Creating Overloaded Functions

要创建重载函数，你只需编写多个具有相同名称但参数列表不同的函数定义即可。在 Triple 程序中，我为函数 triple() 编写了两个定义，每个定义都指定了不同的类型作为其单个参数。以下是函数原型：

```
int triple(int number);
string triple(string text);
```

第一个接受 int 参数并返回 int。第二个接受 string 对象并返回 string 对象。

在每个函数定义中，你可以看到我返回了发送值的三倍。在第一个函数中，我返回发送的 int 的三倍。在第二个函数中，我返回发送的字符串，重复三次。

## Trap

要实现函数重载，你需要为同一个函数编写多个定义，这些定义具有不同的参数列表。请注意，我没有提到返回类型。那是因为如果你编写两个函数定义，其中只有返回类型不同，你会生成编译错误。例如，你不能在程序中同时具有以下两个原型：

```
int Bonus(int);
float Bonus(int);
```

## Calling Overloaded Functions

你可以像调用任何其他函数一样调用重载函数，使用其名称并提供一组有效参数。但对于重载函数，编译器会根据参数值确定调用哪个定义。例如，当我用以下行调用 triple() 并使用 int 作为参数时，编译器知道要调用接受 int 的定义。因此，函数返回 int 15。

```
cout << "Tripling 5: " << triple(5) << "\n\n";
```

我再次调用 triple()：

```
cout << "Tripling 'gamer': " << triple("gamer");
```

因为我使用字符串字面量作为参数，编译器知道要调用接受 string 对象的函数定义。因此，函数返回字符串对象 equal to gamergamergamer。

## INLINING FUNCTIONS

调用函数会带来少量性能开销。通常这不是大问题，因为开销相对较小。然而，对于微小的函数（例如一两行），有时可以通过内联它们来加快程序性能。通过内联函数，你要求编译器在每次调用的地方都复制一份函数。因此，程序控制不必每次调用函数时都跳转到不同的位置。

## Introducing the Taking Damage Program

Taking Damage 程序模拟了角色在受到辐射伤害时生命值的变化。角色每轮损失一半的生命值。幸运的是，程序只运行三轮，所以我们免于角色悲惨结局的困扰。程序内联了计算角色新生命值的微小函数。Figure 5.7 显示了程序结果。

你可以在 Course Technology 网站 (www.courseptr.com/downloads) 上下载此程序的代码。该程序位于 Chapter 5 文件夹中；文件名是 taking_damage.cpp。

![](img/34f09be0ed6217c465debc4490197d4f_200_0.png)

## Figure 5.7

角色以相当高效的方式接近死亡，他的生命值通过内联函数减少。

```
// Taking Damage
// Demonstrates function inlining

#include <iostream>

int radiation(int health);

using namespace std;

int main()
{
    int health = 80;
    cout << "Your health is " << health << "\n\n";

    health = radiation(health);
    cout << "After radiation exposure your health is " << health << "\n\n";

    health = radiation(health);
    cout << "After radiation exposure your health is " << health << "\n\n";

    health = radiation(health);
    cout << "After radiation exposure your health is " << health << "\n\n";
```
right at this place in the program. In fact, the compiler does this for all three calls to the function.

## Real World

虽然痴迷于性能是游戏程序员最喜欢的爱好，但在速度上过度关注是有危险的。事实上，许多开发人员采取的方法是先让他们的游戏程序运行良好，然后再为微小的性能提升进行调整。此时，程序员会 *profile* 他们的代码，通过运行一个分析游戏程序花费时间位置的实用程序（分析器）。如果程序员看到瓶颈，他或她可能会考虑诸如函数内联之类的手工优化。

## INTRODUCING THE MAD LIB GAME

Mad Lib 游戏要求用户帮助创建故事。用户提供一个人的名字、一个复数名词、一个数字和一个动词。程序收集所有这些信息并用它来创建个性化故事。Figure 5.8 显示了程序的示例运行。

![](img/34f09be0ed6217c465debc4490197d4f_202_0.png)

Figure 5.8

用户提供所有必要信息后，程序会显示文学杰作。

```
tellStory(name, noun, number, bodyPart, verb);

    return 0;
}
```

## The askText() Function

askText() 函数从用户获取一个字符串。该函数用途广泛，接受一个 string 类型的参数，用作提示用户。因此，我能够调用此单个函数来要求用户提供各种不同的信息，包括名字、复数名词、身体部位和动词。

```
string askText(string prompt)
{
    string text;
    cout << prompt;
    cin >> text;
    return text;
}
```

## Trap

请记住，cin 的这种简单用法仅适用于没有空白字符的字符串（例如制表符或空格）。因此，当用户被提示输入身体部位时，他可以输入 bellybutton，但 medulla oblongata 会导致程序出现问题。

有办法补偿这一点，但这确实需要讨论一种称为流的东西，这超出了本书的范围。所以以这种方式使用 cin，但要意识到其局限性。

## The askNumber() Function

askNumber() 函数从用户获取一个整数。虽然我在程序中只调用它一次，但它用途广泛，因为它接受一个 string 类型的参数，用作提示用户。

```
int askNumber(string prompt)
{
    int num;
    cout << prompt;
    cin >> num;
    return num;
}
```

- 你可以使用 `return` 语句从函数返回一个值。你也可以使用 `return` 来结束返回类型为 `void` 的函数。
- 变量的作用域决定了变量在程序中可以在哪里被看到。
- 全局变量可以从程序的任何部分访问。一般来说，你应该尽量限制对全局变量的使用。
- 全局常量可以从程序的任何部分访问。使用全局常量可以使程序代码更清晰。
- 默认参数在函数调用中未为参数指定值时会被分配给参数。
- 函数重载是为同一个函数创建多个定义的过程，每个定义的参数集都不同。
- 函数内联是要求编译器内联函数的过程——意味着编译器应该在代码中函数被调用的每个地方都复制一份函数。内联非常小的函数有时可以带来性能提升。

## QUESTIONS AND ANSWERS

Q: 为什么我应该编写函数？

A: 函数允许你将程序分解为逻辑块。这些块产生更小、更易管理的代码块，比单个庞大的程序更容易处理。

Q: 什么是封装？

A: 从核心来看，封装是关于保持事物分离。例如，函数封装提供了一个功能，即在函数中声明的变量在函数外部不可访问。

Q: 参数和参数有什么区别？

A: 参数是你在使用函数调用向函数传递值时使用的。参数是你在使用函数定义接受传递给函数的值时使用的。

