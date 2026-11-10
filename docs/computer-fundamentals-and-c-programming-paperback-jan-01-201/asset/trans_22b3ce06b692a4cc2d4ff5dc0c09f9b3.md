
```text
Enter a valid number for operator: 3
40.000000

Enter left operand: 10.5
Enter right operand: 20.3
1. '+' 2. '-' 3. '*' 4. '/' 5. '%'
Enter a valid number for operator: 1
30.799999

Enter left operand: 20
Enter right operand: 40
1. '+' 2. '-' 3. '*' 4. '/' 5. '%'
Enter a valid number for operator: 6
Illegal operator
[Ctrl-C]                         Terminates program abnormally
```

程序输出：`calculator.c`

三个 `scanf` 语句使运算符及其操作数可供 `switch` 结构使用。每个专门对应一个运算符的 `case` 选项都会打印该运算的结果。前五个 `case` 选项中的 `break` 确保一旦找到匹配项，控制流不会向下贯穿。请注意，取模运算符需要强制类型转换，因为它只适用于整数操作数。该程序存在缺陷；本应有一个单独的选项（例如 0 或 9），让程序可以通过 `return` 语句优雅地退出。

## 7.17 `mobile_tariffs.c`：计算 4G 服务费用的程序

下一个程序（程序 7.8）让你评估移动运营商提供的 4G 上网套餐。数据取自 7.7 节中展示的代码片段。程序提供一个包含四种套餐的菜单供选择，然后使用 `switch` 将所提供的流量（以 GB 为单位）和套餐价格赋给两个变量。接着，它显示所选套餐的每单位费率。程序在一个无限循环中运行，当遇到 `return` 语句时终止。

```c
/* mobile_tariffs.c: Computes the cost per GB of data consumed from among
   four 4G Internet plans. Uses a multi-line printf to display a menu. */
#include <stdio.h>
int main(void)
{
    short option, data_limit, tariff;

    while (1) {
        printf("\nChoose from the following 4G plans:\n\n"
               "\t1. 1 GB for Rs 255\n\t2. 2 GB for Rs 455\n"
               "\t3. 4 GB for Rs 755\n\t4. 10 GB for Rs 995\n"
               "\t9. Exit"
               "\nEnter choice: ");
        scanf("%hd", &option);

        switch (option) {
            case 1: data_limit = 1; tariff = 255;
                break;
            case 2: data_limit = 2; tariff = 455;
                break;
            case 3: data_limit = 4; tariff = 755;
                break;
            case 4: data_limit = 10; tariff = 995;
                break;
            case 9: printf("Quitting ...\n");
                return 0;
            default: printf("Invalid option\n");
        }

        if (option >= 1 && option <= 4) {
            printf("You chose %d GB for Rs %d.\n", data_limit, tariff);
            printf("Cost per GB = Rs %.2f\n", (float) tariff / data_limit);
        }
            /* Closes while */
}
```

程序 7.8：**mobile_tariffs.c**

```text
Choose from the following 4G plans:

    1. 1 GB for Rs 255
    2. 2 GB for Rs 455
    3. 4 GB for Rs 755
    4. 10 GB for Rs 995
    9. Exit
Enter choice: 4
You chose 10 GB for Rs 995.
Cost per GB = Rs 99.50

Choose from the following 4G plans:

    1. 1 GB for Rs 255
    2. 2 GB for Rs 455
    3. 4 GB for Rs 755
    4. 10 GB for Rs 995
    9. Exit
Enter choice: 9
Quitting ...
```

程序输出：**mobile_tariffs.c**

观察单个 **printf** 语句如何借助 `\t` 和 `\n` 转义序列创建一个包含五个选项的多行菜单。用户的选择由 **switch** 用来设置变量 `data_limit` 和 `tariff`。当用户选择 9 时，程序优雅地终止。

## 7.18 `date_validation.c`：验证日期的程序

程序 7.9 使用两个 **switch** 结构来验证以 *dd/mm/yyyy* 格式输入的日期。第一个 **switch** 验证月份，第二个 **switch** 验证日。该程序有两个有趣的特性——在某些 **case** 选项中省略了 **break**，以及在 **switch** 内部使用 **continue** 语句，尽管 **continue** 并不属于 **switch** 结构的一部分。

```c
/* date_validation.c: Validates a date that is input in dd/mm/yyyy format.
   Uses continue inside switch and drops break from some labels. */

#include <stdio.h>

int main(void)
{
    short day, month, year, max_days;

    while (1) {
        printf("Enter date in dd/mm/yyyy format: ");
        scanf("%hd/%hd/%hd", &day, &month, &year);

        /* Month validated & max days set here */
        switch (month) {
            case 2 : max_days = (year % 4 == 0) &&
                               (year % 100 != 0 || year % 400 == 0) ? 29 : 28;
                     break;
            case 4 :                    /* Fall-through from case 4 to case 11 */
            case 6 :
            case 9 :
            case 11 : max_days = 30;    /* Applies to case 4, 6, 9 and 11 */
                      break;
            default : if (month > 12) {
                          printf("Illegal month\n");
                          continue;
                      }
                      max_days = 31;   /* For the remaining 7 months */
        }

        /* Day validated here */
        switch (day > max_days) {    /* Relational expression used here */
            case 1 : printf("Illegal number of days\n");
                     continue;
            case 0 : printf("Valid date\n");
        }
        return 0;                    /* Program terminates if date valid */
    }                                /* Closes while loop */
}                                    /* Closes main */
```

程序 7.9：**date_validation.c**

```text
Enter date in dd/mm/yyyy format: 31/06/2016
Illegal number of days
Enter date in dd/mm/yyyy format: 30/13/2015
Illegal month
Enter date in dd/mm/yyyy format: 29/02/1900
Illegal number of days
Enter date in dd/mm/yyyy format: 29/02/2000
Valid date
```

程序输出：`date_validation.c`

这个程序看起来可能令人生畏，但实际上相当简单。它首先从 `scanf` 保存的输入中提取月份并进行验证。第一个 `switch` 将 12 个月分为三类：二月、四个 30 天的月份和七个 31 天的月份。二月首先使用先前讨论过的逻辑表达式检查是否为闰年。

接下来，30 天的月份由四个 `case` 选项处理，其中三个指定不执行任何操作且没有 `break`。对于这三个选项，控制流会一直向下贯穿，直到在标记为 11 的 `case` 中遇到 `break` 为止。此处执行的赋值 `max_days = 30` 同样适用于前三个选项。如果 `switch` 不支持在缺少 `break` 时的默认贯穿行为，这是不可能实现的。

剩余的七个 31 天月份由 `default` 标签处理，其中包含两个 `continue` 语句中的第一个。与 `break` 不同，`continue` 不是 `switch` 语法的一部分。它在所有循环中用于从循环顶部重新开始下一次 *迭代*（用来描述遍历循环中所有语句的术语）。在这个程序中，`continue` 只是重新启动 `while` 循环。现在可以安全地将 `max_days` 设置为 31。

第二个 `switch` 只是检查输入的日是否超过 `max_days`。这里也有 `continue`，以便在输入无效日时给用户另一次机会。当输入有效日期时，程序通过 `return 0;` 正常终止。

> 要点：`break` 和 `continue` 都会终止 `switch`，但 `continue` 仅在 `switch` 被循环包含时有效。`break` 将控制权转移到 `switch` 结束符（闭合的控制花括号）之后的语句，而 `continue` 将控制权转移到循环顶部，开始下一次迭代。

## 7.19 “无限可滥用”的 goto 语句

`break` 和 `continue` 都可以视为 Fortran 和 BASIC 等语言提供的 GOTO 语句的受限版本。然而，C 也支持 `goto` 语句，它允许控制流分支到程序中的另一个点，而无需返回到程序中执行它的位置。自从 Kernighan 和 Ritchie 提出这个“无限可滥用”的结构应该“如果非要用，也应尽量节制”以来，围绕该语句出现了大量负面宣传。在我们自己获得教训之前，先来看一个使用 `goto` 的小程序（程序 7.10）。
