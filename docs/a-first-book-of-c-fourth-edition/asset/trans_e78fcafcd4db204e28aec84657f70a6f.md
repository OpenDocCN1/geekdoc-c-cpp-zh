

你的第一反应可能是“程序明确要求你输入整数值”。然而，有经验的程序员明白，他们的责任是确保程序能够预见并妥善处理用户可能输入的任何数据。为了实现这一目标，在开发程序时思考可能会出现什么问题，然后让另一人或一组人彻底测试程序。¹

处理无效数据输入的基本方法称为用户输入验证，这意味着在数据输入时或输入后立即检查所输入的数据，然后为用户提供重新输入任何无效数据的方式。用户输入验证是任何具有商业价值程序不可或缺的一部分；如果做得正确，它可以保护程序免于尝试处理可能导致计算问题的<|message|>数据。你将在第 4 章和第 5 章学习 C++ 的选择语句和重复语句时看到这种验证类型的操作方法。

## EXERCISES 3.4

- 1. (Practice) 对于以下声明语句，编写一个或多个使用 cin 对象的语句，使计算机在用户输入适当数据时暂停：
- a. int firstnum;
- b. double grade;
- c. double secnum;
- d. char keyval;
- e. int month, years;
    double average;
- f. char ch;
    int num1,num2;
    double grade1,grade2;
- g. double interest, principal, capital;
    double price, yield;
- h. char ch, letter1,letter2;
    int num1,num2,num3;
- i. double temp1,temp2,temp3;
    double volts1,volts2;

- 2. (Program) a. 编写、编译并运行一个 C++ 程序，显示以下提示：
Enter the length of the room:
Enter the width of the room:
在显示每个提示后，你的程序应使用 cin 对象调用从键盘接受与所显示提示对应的数据。在输入房间宽度后，你的程序应计算并显示房间面积。显示的面积应使用公式 area = length × width 计算，并包含在适当的提示信息中。
b. 通过手动计算结果来检查为练习 2a 编写的程序所显示的面积。

### 3. (Program) a. 编写、编译并运行一个 C++ 程序，显示以下提示：

Enter the length of the swimming pool:
Enter the width of the swimming pool:
Enter the average depth of the swimming pool:

在显示每个提示后，你的程序应使用 cin 语句从键盘接受与所显示提示对应的数据。在输入游泳池深度后，你的程序应计算并显示池水的体积。体积应使用公式 volume = length × width × average depth 计算并在输出信息中显示。

b. 通过手动计算结果来检查为练习 3a 编写的程序所显示的体积。

### 4. (Program) 编写、编译并运行一个 C++ 程序，显示以下提示：

Enter the radius of a circle:

在接受半径值后，你的程序应计算并显示圆的面积。提示：Area = 3.1416 × radius²。）为测试目的，通过使用输入半径为 3 英寸来验证你的程序。在手动确定你的程序结果正确后，使用你的程序完成以下图表：

| Radius (in) | Area (sq. in) |
|---|---|
| 1.0 | |
| 1.5 | |
| 2.0 | |
| 2.5 | |
| 3.0 | |
| 3.5 | |

### 5. (Program) a. 编写一个 C++ 程序，首先显示以下提示：

Enter the temperature in degrees Celsius:

让你的程序接受从键盘输入的值并将其转换为华氏度，使用以下公式：

Fahrenheit = (9.0 / 5.0) × Celsius + 32.0

你的程序随后应使用输出信息显示华氏温度。

b. 编译并运行为练习 5a 编写的程序。为验证你的程序，使用以下测试数据并手工计算华氏等价值，然后使用你的程序查看是否得到相同的结果：

- Test data set 1: 0 degrees Celsius
- Test data set 2: 50 degrees Celsius
- Test data set 3: 100 degrees Celsius

当你确信你的程序工作正确时，使用它完成以下图表：

| Celsius | Fahrenheit |
| 45 |  |
| 50 |  |
| 55 |  |
| 60 |  |
| 65 |  |
| 70 |  |

### 6. (Program) a. 编写、编译并运行一个 C++ 程序，显示以下提示：

```
Enter the miles driven:
Enter the gallons of gas used:
```

在显示每个提示后，你的程序应使用 cin 语句从键盘接受与所显示提示对应的数据。在输入汽油使用量后，你的程序应计算并显示每加仑英里数 mpg。此值应使用公式 miles per gallon = miles / gallons used 计算并在输出信息中显示。通过使用以下测试数据验证你的程序：
Test data set 1: miles = 276, gas = 10 gallons
Test data set 2: miles = 200, gas = 15.5 gallons

完成验证后，使用你的程序完成以下图表。确保将行驶英里数转换为行驶公里数，将使用的加仑数转换为使用的升数，然后计算每升公里数。每英里有 1.61 公里，每加仑有 4.54609 升。）

| Miles Driven | Gallons Used | Mpg | Km Driven | Liters Used | Km/L |
| 250 | 16.00 |  |  |  |  |
| 275 | 18.00 |  |  |  |  |
| 312 | 19.54 |  |  |  |  |
| 296 | 17.39 |  |  |  |  |

b. 对于练习 6a 编写的程序，确定需要多少次验证运行才能确保程序工作正确，并给出支持你的答案的理由。

### 7. (Program) a. 编写、编译并运行一个 C++ 程序，显示以下提示：

```
Enter a number:
Enter a second number:
Enter a third number:
Enter a fourth number:
```

在显示每个提示后，你的程序应使用 cin 语句从键盘接受一个数字作为所显示提示的输入。在输入第四个数字后，你的程序应计算并显示这些数字的平均值。平均值应

在输出信息中显示。通过使用以下测试数据检查你的程序计算的平均值：

- Test data set 1: 100, 100, 100, 100
- Test data set 2: 100, 0, 100, 0

完成验证后，使用你的程序完成以下图表：

| Numbers | Average |
|---|---|
| 92, 98, 79, 85 | |
| 86, 84, 75, 86 | |
| 63, 85, 74, 82 | |

b. 重复练习 7a，确保对每个数字输入使用相同的变量名 number。另使用变量 sum 表示数字之和。提示：为此，你可以在每次接受数字后使用语句 sum = sum + number;。复习第 3.1 节中关于累加的材料。

### 8. (Program) 地下泳池的周长、近似表面积和近似体积由以下公式给出：

perimeter = 2 × (length + width)
volume = length × width × average depth
underground surface area = 2 × (length + width) × average depth + length × width

以这些公式为基础，编写一个 C++ 程序，接受长度、宽度和平均深度测量值，然后计算泳池的周长、体积和地下表面积。在编写程序时，在输入数据后立即进行这两个计算：length × width 和 length + width。这两个计算的结果应根据需要在确定周长、体积和地下表面积的赋值语句中使用，而无需为每个方程重新计算。通过手工计算验证你的程序结果，使用以下测试数据：length = 25 feet, width = 15 feet, and average depth = 5.5 feet。在验证程序工作正常后，使用它完成以下图表：

| Length | Width | Average Depth | Perimeter | Volume | Underground Surface Area |
|---|---|---|---|---|---|
| 25 | 10 | 5.0 | | | |
| 25 | 10 | 5.5 | | | |
| 25 | 10 | 6.0 | | | |
| 25 | 10 | 6.5 | | | |
| 30 | 12 | 5.0 | | | |
| 30 | 12 | 5.5 | | | |
| 30 | 12 | 6.0 | | | |
| 30 | 12 | 6.5 | | | |

