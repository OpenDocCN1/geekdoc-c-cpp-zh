
接下来定义的 `initializeScreen` 函数只是向屏幕发送一个换行命令：

```
void initializeScreen()
{
    cout << endl;
}
```

如果你的程序将下面对该函数的调用作为第一条可执行语句，那么之前运行的程序所产生的输出将与你的程序的输出分隔开：

```
initializeScreen();
```

请务必注意，即使函数没有参数，在函数声明和函数调用中仍然必须包含括号。

对于 void 函数，函数声明（函数原型）和函数定义的位置与我们之前描述的有返回值函数的情况相同。

## void 函数中的 return 语句

void 函数和返回值函数都可以有 return 语句。对于返回值函数，return 语句指定返回的值。对于 void 函数，return 语句不包含任何返回值表达式。void 函数中的 return 语句只是结束函数调用。每个返回值函数必须通过执行 return 语句来结束。然而，void 函数不需要包含 return 语句。如果它不包含 return 语句，它将在执行完函数体中的代码后结束。就像在函数体末尾的最终右花括号 `}` 之前有一个隐式的 return 语句一样。

函数体末尾右花括号之前有隐式 return 语句这一事实并不意味着在 void 函数中永远不需要 return 语句。例如，显示 3.7 中的函数定义可能是餐厅管理程序的一部分。该函数输出关于如何在餐桌旁的人群中分配给定数量冰淇淋的指令。如果餐桌旁没有人（即，如果 `number` 等于 0），那么 `if` 语句中的 return 语句将终止函数调用并避免除以零。如果 `number` 不为 0，那么当函数体末尾的最后一条 `cout` 语句执行时，函数调用结束。

## 前置条件和后置条件

编写函数声明注释的一个好方法是将其分解为两类信息，称为前置条件和后置条件。前置条件说明调用函数时假设什么为真。除非前置条件成立，否则不应使用该函数，也不能指望它正确执行。后置条件描述函数调用的效果；也就是说，后置条件说明在前置条件成立的情况下执行函数后什么将变为真。对于返回值函数，后置条件将描述函数返回的值。对于改变某些参数变量值的函数，后置条件将描述对参数值所做的所有更改。

### 显示 3.7 在 void 函数中使用 return

```
1 #include <iostream>
2 using namespace std;
3 void iceCreamDivision(int number, double totalWeight);
4 //Outputs instructions for dividing totalWeight ounces of ice cream
5 //among number customers. If number is 0, only an error message is output.
6 int main()
7 {
8     int number;
9     double totalWeight;
10     cout << "Enter the number of customers: ";
11     cin >> number;
12     cout << "Enter weight of ice cream to divide (in ounces): ";
13     cin >> totalWeight;
14     iceCreamDivision(number, totalWeight);
15     return 0;
16 }
17 void iceCreamDivision(int number, double totalWeight)
18 {
19     double portion;
20     if (number == 0)
21     {
22         cout << "Cannot divide among zero customers.\n";
23         return;
24     }
25     portion = totalWeight/number;
26     cout << "Each one receives "
27         << portion << " ounces of ice cream." << endl;
28 }
```

如果 `number` 为 0，则函数执行在此结束。

### 示例对话

```
Enter the number of customers: 0
Enter weight of ice cream to divide (in ounces): 12
Cannot divide among zero customers.
```

例如，下面是一个带有前置条件和后置条件的函数声明：

```
void showInterest(double balance, double rate);
//Precondition: balance is a nonnegative savings account balance.
//rate is the interest rate expressed as a percentage, such as 5
//for 5%.
//Postcondition: The amount of interest on the given balance
//at the given rate is shown on the screen.
```

使用这个函数并不需要知道函数 `showInterest` 的定义。使用该函数所需知道的一切都由前置条件和后置条件给出。

当唯一的后置条件是对返回值的描述时，程序员通常会省略“Postcondition”一词，如下例所示：

```
double celsius(double fahrenheit);
//Precondition: fahrenheit is a temperature in degrees
//Fahrenheit.
//Returns the equivalent temperature expressed in degrees
//Celsius.
```

有些程序员选择在函数注释中不使用“precondition”和“postcondition”这两个词。然而，无论你是否使用这些词，在设计函数以及决定函数注释中包含什么内容时，你都应该始终从前置条件和后置条件的角度来思考。

## main 是一个函数

正如我们已经指出的，程序的主要部分实际上是一个名为 `main` 的函数的定义。程序运行时，函数 `main` 会被自动调用；它转而又可能调用其他函数。尽管程序主要部分中的 return 语句看起来似乎是可以选的，但实际上并非如此。C++ 标准规定你可以省略程序主要部分中的 `return 0` 语句，但许多编译器仍然要求它，而且几乎所有编译器都允许你包含它。为了可移植性，你应该在 `main` 函数中包含 `return 0` 语句。你应该将程序的主要部分视为一个返回 `int` 类型值的函数，因此需要 return 语句。将程序的主要部分视为返回整数的函数可能听起来很奇怪，但这是许多编译器强制遵循的传统。

尽管有些编译器可能允许你这样做而不受惩罚，但你不应该在代码中包含对 `main` 的调用。只有系统才应该调用 `main`，而系统会在你运行程序时这样做。

## 递归函数

C++ 确实允许你定义递归函数。递归函数在第 13 章中介绍。如果你不知道递归函数是什么，那么在读到那一章之前不必担心。如果你想提前阅读递归函数，可以在完成第 4 章后阅读第 13 章的 13.1 和 13.2 节。注意，`main` 函数不应被递归调用。

## 自测练习

- 15. 下面程序的输出是什么？

    ```
    #include <iostream>
    using namespace std;
    void friendly( );
    void shy(int audienceCount);
    int main()
    {
        friendly( );
        shy(6);
        cout << "One more time:\n";
        shy(2);
        friendly( );
        cout << "End of program.\n";
        return 0;
    }
    void friendly()
    {
        cout << "Hello\n";
    }
    void shy(int audienceCount)
    {
        if (audienceCount < 5)
            return;
        cout << "Goodbye\n";
    }
    ```

- 16. 假设你在显示 3.7 的 `iceCreamDivision` 函数定义中省略了 return 语句。这对程序会有什么影响？程序能编译吗？它能运行吗？程序的行为会有什么不同吗？

- 17. 为一个 void 函数编写定义，该函数有三个 `int` 类型的参数，并在屏幕上输出这三个参数的乘积。将定义放在一个完整的程序中，该程序读取三个数字然后调用这个函数。

- 18. 你的编译器是否允许 `void main( )` 和 `int main( )`？如果你使用 `int main( )` 但未提供 `return 0;` 语句，会发出什么警告？要查明这一点，请编写几个小的测试程序，或者咨询你的老师或当地的专家。

- 19. 为预定义函数 `sqrt` 给出前置条件和后置条件，该函数返回其参数的平方根。

