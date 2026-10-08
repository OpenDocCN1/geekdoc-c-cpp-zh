

## 实践练习

- Q1. 编写一个程序，使用条件运算符求两个整数的最大值。
- Q2. 编写一个程序，使用条件运算符求三个整数的最大值。
- Q3. 编写一个程序，使用取模运算符和条件运算符判断输入的数字是奇数还是偶数。
- Q4. 编写一个程序，接受十六进制整数并打印其十进制等价值。
- Q5. 编写一个程序，计算支付给员工（基本工资为 25,000 卢比）的净工资，工资明细如下：
  公司以以下科目形式提供激励：
  DA（津贴）= 基本工资的 48%，HRA（住房津贴）= 基本工资的 15%，CA（附加工资）= 基本工资的 5%，MA（月津贴）= 500 卢比。
  公司以以下科目形式扣除金额：
  PF（养老金）=（基本工资 + DA）的 8.33%，专业税 = 100
  用于计算工资的公式为：净工资 = 基本工资 + DA + HRA + CA + MA –（PF + 专业税）
- Q6. 编写一个程序，计算接受的小数小时和分钟值代表的总分钟数。
- Q7. 编写一个 C 程序，接受用户输入的年份数，并将其显示为月份和天数。
- Q8. 编写一个程序，输入两个数字 i_first 和 i_second。检查数字 i_first 是否能被数字 i_second 整除。（不要使用 % 运算符）
- Q9. 二次函数的形式为 f(x) = ax² + bx + c。编写一个程序，接受 a、b、c 和 x 的值来求 f(x) 的值。
- Q10. 编写一个程序，接受三个整型变量 i_first、i_second 和 i_num。
  将变量 i_first 右移 i_num 位，并将变量 i_second 左移 i_num 位。

## 06
C 语言中的序列控制

## 目标

- 解释决策结构

我们在本书第 1 章中提到，程序总是按从上到下的顺序执行的。语句按其在 C 程序中出现的顺序依次逐个执行。一旦当前语句执行完毕，编译器默认将控制权转移到下一条语句。在实际场景中，这种顺序流程行不通。我们有时需要根据某些条件改变执行顺序，或者可能需要重复执行特定的语句集合。在本章中，我们将学习用于改变执行流程的控制结构。这种控制结构称为决策结构。我们还将讨论决策结构的不同变体，并了解如何在程序中使用它们。

### 6.1
决策结构

C 语言的决策结构用于进行选择。选择允许我们从程序内的两个或多个可用选项中选择一项。在 C 语言中，决策结构允许我们根据一个或多个条件的结果执行预定义的操作。C 语言提供两种类型的选择语句，称为双向选择和多向选择。下一节讨论双向选择。

### 双向选择

C 语言中的双向选择代表一个条件语句，该语句可以被编译器评估为真或假。如果答案为真，则执行一个或多个操作语句。如果答案为假，则执行另一组操作语句。双向选择的一般流程图如图 1 所示：

![](img/5d422ba7108ffdf64376be51eaf0c459_118_0.png)

图 1：双向选择的流程图

从图 1 可以看出，无论执行哪一组操作语句，C 编译器在选择之后都会继续执行下一条语句。双向选择在 C 中使用 *if* 和 *else* 关键字实现。

关键字 *if* 用于控制权的条件转移。它与可以评估为真或假的表达式结合使用。*if* 语句有三种变体，分别称为简单 *if* 语句、*if-else* 语句和嵌套 *if* 语句。它们各自用于不同的情况。下一个小节讨论简单 *if* 语句的用法。

### 简单 If 语句

简单 if 语句表示仅在指定条件为真时采取行动，而在条件为假时不采取行动的情况。简单 if 语句的语法如下：

```
if ( 测试条件 )
操作语句;
```

从上述语法可以看出，测试条件总是写在括号内。它通常是一个产生整数值 的表达式。任何非零值代表真，而零值代表假。测试条件不以分号结束。如果使用分号，条件语句将转换为*空语句*。从执行的角度来看，空语句没有任何意义。默认情况下，*if* 语句的作用域是紧接在测试条件之后的那条语句。为了将 *if* 语句的作用域扩展到多个语句，我们需要使用开括号和闭括号将这些语句包围起来。当语句嵌入在开括号和闭括号内时，称为复合语句。图 2 说明了简单 *if* 语句的逻辑流程：

![](img/5d422ba7108ffdf64376be51eaf0c459_119_0.png)

图 2：简单 If 语句的逻辑流程

从图 2 可以看出，首先会评估测试条件。如果测试条件的值为正的非零值（真），则控制权转移到真操作语句块中的第一条语句。然后执行真操作块内的语句。如果测试条件的值为零，*则* 不采取任何行动。控制权的转移发生在真操作块完成后，或者在不采取行动的情况下，转移到 *if* 之后顺序中的下一条语句。程序 1 说明了简单 *if* 语句的使用：

#### 程序 1

```c
/** 用于说明简单 if 语句用法的程序 */
#include<stdio.h>
/** 主函数开始 */
main()
{
    /** 声明变量 */
    float f_purchase, f_discount = 0.0;
    float f_dis_amount, f_payment;
    
    /** 读取值 */
    printf("\nEnter total purchase amount: ");
    scanf("%f", &f_purchase);
    
    /** 计算折扣金额 */
    if (f_purchase >= 5000.00)
        f_discount = 0.15;
    
    f_dis_amount = f_purchase * f_discount;
    
    /** 计算支付金额 */
    f_payment = f_purchase - f_dis_amount;
    
    /** 输出数据 */
    printf("\nTotal payment to be made Rs. %.2f\n", f_payment);
    printf("Total discount availed Rs. %.2f\n", f_dis_amount);
    
    return;
}
/** 主函数结束 */
```

#### 输出 1：

```
Enter total purchase amount: 7500
Total payment to be made Rs. 6375.00
Total discount availed Rs. 1125.00
```

#### 输出 2：

```
Enter total purchase amount: 4500
Total payment to be made Rs. 4500.00
Total discount availed Rs. 0.00
```

从程序 1 可以看出，该程序用于计算在购买金额达到或超过 5000 卢比时的折扣。在这里，语句 if (f_purchase >= 5000.00) 是决策结构，如果测试条件为真，则给 f_discount 分配一个新值。两个输出表明，在第一种情况下，新值（0.15）被分配给 f_discount，而在第二种情况下，使用旧值（0.00）。

请注意，在程序 1 的测试条件中，我们使用了关系运算符（>=）。我们可以在测试条件中使用任何有效的 C 运算符，例如关系运算符、逻辑运算符、逗号、赋值运算符或其他运算符。程序 2 说明了在简单 if 语句中结合使用逻辑运算符和关系运算符：

#### 程序 2

```c
/* 用于说明简单 if 语句用法的程序 */
#include<stdio.h>

/* 主函数开始 */
main()
{
    /* 声明变量 */
    float f_purchase, f_discount = 0.0;
    float f_dis_amount, f_payment;
    char c_regular, c_temp;
    /* 读取值 */
    printf("\nEnter total purchase amount: ");
    scanf("%f", &f_purchase);
    c_temp = getchar();
    printf("Enter Y or y if regular customer: ");
    scanf("%c", &c_regular);

    /* 计算折扣金额 */
    if (f_purchase >= 5000.00 && (c_regular == 'y' || c_regular == 'Y'))
        f_discount = 0.15;

    f_dis_amount = f_purchase * f_discount;
    /* 计算支付金额 */
    f_payment = f_purchase - f_dis_amount;

    /* 输出数据 */
    printf("\nTotal payment to be made Rs. %.2f\n", f_payment);
    printf("Total discount availed Rs. %.2f\n", f_dis_amount);

    return;
    /* 主函数结束 */
}
```

#### 输出 1：

```
Enter total purchase amount: 7500

Enter Y or y if regular customer: y

Total payment to be made Rs. 6375.00

Total discount availed Rs. 1125.00
```

#### 输出 2：

```
Enter total purchase amount: 7500

Enter Y or y if regular customer: n

Total payment to be made Rs. 7500.00

Total discount availed Rs. 0.00
```

从程序 2 可以看出，我们同时使用了关系运算符和逻辑运算符。图 3 展示了 if 语句中测试条件的评估方式：

