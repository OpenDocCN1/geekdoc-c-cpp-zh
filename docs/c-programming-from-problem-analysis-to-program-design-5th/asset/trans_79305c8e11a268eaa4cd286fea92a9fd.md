
下面的 C++ 程序展示了前面输入语句的效果：

```cpp
// This program illustrates how input statements work.

#include <iostream>

using namespace std;

int main()
{
    int feet;
    int inches;

    cout << "Enter two integers separated by spaces: ";
    cin >> feet >> inches;
    cout << endl;

    cout << "Feet = " << feet << endl;
    cout << "Inches = " << inches << endl;

    return 0;
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```
Enter two integers separated by spaces: 23 7

Feet = 23
Inches = 7
```

示例 2-18 中的 C++ 程序说明了如何读取字符串和数值数据。

## 示例 2-18

```cpp
// This program illustrates how to read strings and numeric data.

#include <iostream>
#include <string>

using namespace std;

int main()
{
    string firstName;                         //Line 1
    string lastName;                          //Line 2
    int age;                                   //Line 3
    double weight;                             //Line 4

    cout << "Enter first name, last name, age, "
         << "and weight, separated by spaces."
         << endl;                             //Line 5

    cin >> firstName >> lastName;                 //Line 6
    cin >> age >> weight;                         //Line 7

    cout << "Name: " << firstName << " "
         << lastName << endl;                     //Line 8

    cout << "Age: " << age << endl;              //Line 9
    cout << "Weight: " << weight << endl;        //Line 10

    return 0;                                     //Line 11
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```
Enter first name, last name, age, and weight, separated by spaces.
Sheila Mann 23 120.5
Name: Sheila Mann
Age: 23
Weight: 120.5
```

上述程序的工作方式如下：第 1 行到第 4 行的语句声明了 string 类型的变量 `firstName` 和 `lastName`、`int` 类型的变量 `age` 以及 `double` 类型的变量 `weight`。第 5 行的语句是一条输出语句，告诉用户该做什么。（此类输出语句称为提示行。）如示例运行所示，程序的输入为：

```
Sheila Mann 23 120.5
```

第 6 行的语句首先读取字符串 Sheila 并将其存入变量 `firstName`，然后跳过 Sheila 后面的空格，读取字符串 Mann 并将其存入变量 `lastName`。接下来，第 7 行的语句首先跳过 Mann 后面的空白，读取 23 并将其存入变量 `age`，然后跳过 23 后面的空白，读取 120.5 并将其存入变量 `weight`。

第 8、9 和 10 行的语句生成示例运行结果的第三、第四和第五行。

> **注意** 在程序执行期间，如果在一行中输入多个值，这些值之间必须至少用一个空格或制表符分隔。或者，也可以每行输入一个值。

## 变量初始化

请记住，初始化变量有两种方式：使用赋值语句和使用读取语句。考虑以下声明：

```
int feet;
int inches;
```

![](img/1fbe55537254baeb2b5b7dbaf64956ae_101_0.png)

考虑以下两组代码：

```cpp
(a) feet = 35;
    inches = 6;
    cout << "Total inches = "
         << 12 * feet + inches;
```

```cpp
(b) cout << "Enter feet: ";
    cin >> feet;
    cout << endl;
    cout << "Enter inches: ";
    cin >> inches;
    cout << endl;
    cout << "Total inches = "
         << 12 * feet + inches;
```

在 (a) 中，feet 和 inches 使用赋值语句初始化；在 (b) 中，这些变量使用输入语句初始化。然而，每次执行 (a) 中的代码时，除非你编辑源代码、更改值、重新编译并运行，否则 feet 和 inches 都会被初始化为相同的值。另一方面，在 (b) 中，每次程序运行时，系统都会提示你输入 feet 和 inches 的值。因此，读取语句比赋值语句通用得多。

有时需要使用赋值语句来初始化变量。如果变量仅用于内部计算，而不用于读取和存储数据，则尤其如此。

回想一下，C++ 在声明变量时不会自动初始化变量。有些变量可以在声明时初始化，而另一些变量必须使用赋值语句或读取语句初始化。

> **注意**
> 
> 当程序编译时，一些较新的 IDE 可能会在程序使用某个变量的值但未先正确初始化该变量时给出警告消息。在这种情况下，如果你忽略警告并执行程序，程序可能会异常终止并显示错误消息。

> **注意**
> 
> 假设你想使用输入语句将一个字符存入 `char` 变量。在程序执行期间，当你输入该字符时，不要包含单引号。例如，假设 `ch` 是一个 `char` 变量。考虑以下输入语句：
> 
> ```cpp
> cin >> ch;
> ```
> 
> 如果你想使用这条语句将 K 存入 `ch`，那么在程序执行期间，你只需输入 K。同样，如果你想使用输入语句将一个字符串存入一个 string 变量，那么在程序执行期间，你只需输入该字符串，不要包含双引号。

## 示例 2-19

这个示例进一步说明了赋值语句和输入语句如何操作变量。考虑以下声明：

```cpp
int firstNum, secondNum;
double z;
char ch;
string name;
```

另外，假设以下语句按给定顺序执行：

- 1. `firstNum = 4;`
- 2. `secondNum = 2 * firstNum + 6;`
- 3. `z = (firstNum + 1) / 2.0;`
- 4. `ch = 'A';`
- 5. `cin >> secondNum;`
- 6. `cin >> z;`
- 7. `firstNum = 2 * secondNum + static_cast<int>(z);`
- 8. `cin >> name;`
- 9. `secondNum = secondNum + 1;`
- 10. `cin >> ch;`
- 11. `firstNum = firstNum + static_cast<int>(ch);`
- 12. `z = firstNum - z;`

此外，假设输入为：

```
8 16.3 Jenny D
```

这一行有四个值：8、16.3、Jenny 和 D，每个值之间用一个空格分隔。

现在让我们确定最后一条语句执行后所声明变量的值。为了明确展示某条特定语句如何改变变量的值，下面显示了每条语句执行后变量的值。（在下面的图中，方框中的问号 [?] 表示该方框中的值未知。）

在语句 1 执行之前，所有变量都未初始化，如图 2-2 所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_103_0.png)

**图 2-2** 语句 1 执行前的变量

接下来，我们显示每条语句执行后变量的值。

| 语句执行后 | 变量的值 | 说明 |
|---|---|---|
| 1 | **firstNum:** 4; **secondNum:** ?; **z:** ?; **ch:** ?; **name:** ? | 将 4 存入 firstNum。 |
| 2 | **firstNum:** 4; **secondNum:** 14; **z:** ?; **ch:** ?; **name:** ? | `2 * firstNum + 6 = 2 * 4 + 6 = 14.`<br>将 14 存入 secondNum。 |
| 3 | **firstNum:** 4; **secondNum:** 14; **z:** 2.5; **ch:** ?; **name:** ? | `(firstNum + 1) / 2.0 = (4 + 1) / 2.0 = 5 / 2.0 = 2.5.`<br>将 2.5 存入 z。 |
| 4 | **firstNum:** 4; **secondNum:** 14; **z:** 2.5; **ch:** A; **name:** ? | 将 'A' 存入 ch。 |
| 5 | **firstNum:** 4; **secondNum:** 8; **z:** 2.5; **ch:** A; **name:** ? | 从键盘读取一个数字（即 8）并将其存入 secondNum。这条语句用新值替换 secondNum 的旧值。 |
| 6 | **firstNum:** 4; **secondNum:** 8; **z:** 16.3; **ch:** A; **name:** ? | 从键盘读取一个数字（即 16.3）并将该数字存入 z。这条语句用新值替换 z 的旧值。 |
| 7 | **firstNum:** 32; **secondNum:** 8; **z:** 16.3; **ch:** A; **name:** ? | `2 * secondNum + static_cast<int>(z) = 2 * 8 + static_cast<int>(16.3) = 16 + 16 = 32.` 将 32 存入 firstNum。这条语句用新值替换 firstNum 的旧值。 |
| 8 | **firstNum:** 32; **secondNum:** 8; **z:** 16.3; **ch:** A; **name:** Jenny | 从键盘读取下一个输入 Jenny，并将其存入 name。 |
| 9 | **firstNum:** 32; **secondNum:** 9; **z:** 16.3; **ch:** A; **name:** Jenny | `secondNum + 1 = 8 + 1 = 9.`<br>将 9 存入 secondNum。 |
| 10 | **firstNum:** 32; **secondNum:** 9; **z:** 16.3; **ch:** D; **name:** Jenny | 从键盘读取下一个输入（即 D）并将其存入 ch。这条语句用新值替换 ch 的旧值。 |
