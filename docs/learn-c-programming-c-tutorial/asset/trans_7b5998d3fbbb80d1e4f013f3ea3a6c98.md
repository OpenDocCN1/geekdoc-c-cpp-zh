

这里，具有最高优先级的运算符位于表格顶部，最低优先级的运算符位于底部。在表达式中，优先级较高的运算符会先被求值。

| 类别 | 运算符 | 结合性 |
|---|---|---|
| 后缀 | `() [] -> . ++ --` | 从左到右 |
| 一元 | `+ - ! ~ ++ -- (type)* & sizeof` | 从右到左 |
| 乘法 | `* / %` | 从左到右 |
| 加法 | `+ -` | 从左到右 |
| 移位 | `<< >>` | 从左到右 |
| 关系 | `< <= > >=` | 从左到右 |
| 相等 | `== !=` | 从左到右 |
| 按位与 | `&` | 从左到右 |
| 按位异或 | `^` | 从左到右 |
| 按位或 | `\|` | 从左到右 |
| 逻辑与 | `&&` | 从左到右 |
| 逻辑或 | `\|\|` | 从左到右 |
| 条件 | `?:` | 从右到左 |
| 赋值 | `= += -= *= /= %= >>= <<= &= ^= \|=` | 从右到左 |
| 逗号 | `,` | 从左到右 |

#### 示例

```c
#include <stdio.h>

main()
{
int a = 20;
int b = 10;
int c = 15;
int d = 5;
int e;

e = (a + b) * c / d;    // ( 30 * 15 ) / 5
printf("Value of (a + b) * c / d is : %d\n", e );

e = ((a + b) * c) / d;   // (30 * 15 ) / 5
printf("Value of ((a + b) * c) / d is : %d\n", e );

e = (a + b) * (c / d);   // (30) * (15/5)
printf("Value of (a + b) * (c / d) is : %d\n", e );

e = a + (b * c) / d;    // 20 + (150/5)
printf("Value of a + (b * c) / d is : %d\n", e );

return 0;
}
```

当您编译并执行上述程序时，它会产生以下结果：

> Value of (a + b) * c / d is : 90
> Value of ((a + b) * c) / d is : 90
> Value of (a + b) * (c / d) is : 90
> Value of a + (b * c) / d is : 50

## 10. 决策制定

决策制定结构要求程序员指定一个或多个由程序评估或测试的条件，以及一条或多条在条件判定为真时执行的语句，并可选地在条件判定为假时执行的其他语句。

下面展示的是大多数编程语言中典型的决策制定结构的一般形式：

![](img/6e49c39a6ef9e32d938b03dc613e44f6_53_0.png)

C 编程语言将任何**非零**和**非空**值视为**真**，如果它是**零**或**空**，则视为**假**值。

C 编程语言提供以下类型的决策制定语句。

| 语句 | 描述 |
|---|---|
| if 语句 | **if 语句**由一个布尔表达式后跟一条或多条语句组成。 |
| if...else 语句 | **if 语句**后面可以跟一个可选的**else 语句**，当条件（布尔表达式）为假时执行。 |
| 嵌套 if 语句 | 您可以在另一个 if 或 else if 语句中使用一个 if 或 else if 语句。 |
| switch 语句 | switch 语句允许一个变量与一组值进行相等性测试。 |
| 嵌套 switch 语句 | 您可以在另一个 switch 语句中使用一个 switch 语句。 |

### if 语句

if 语句由一个布尔表达式后跟一条或多条语句组成。

#### 语法

C 编程语言中 `if` 语句的语法是：

```c
if(boolean_expression)
{

    /* statement(s) will execute if the boolean expression is true */

}
```

如果布尔表达式求值为真，则 `if` 语句内部的代码块将被执行。如果布尔表达式求值为假，则 `if` 语句结束（右花括号之后）后的第一组代码将被执行。

C 编程语言将任何非零和非空值视为真，如果它是零或空，则视为假值。

#### 流程图

![](img/6e49c39a6ef9e32d938b03dc613e44f6_54_0.png)

![](img/6e49c39a6ef9e32d938b03dc613e44f6_55_0.png)

#### 示例

```c
#include <stdio.h>

int main ()
{
    /* local variable definition */
    int a = 10;

    /* check the boolean condition using if statement */
    if( a < 20 )
    {
        /* if condition is true then print the following */
        printf("a is less than 20\n" );
    }
    printf("value of a is : %d\n", a);

    return 0;
}
```

当上述代码被编译并执行时，它产生以下结果：

```text
a is less than 20
value of a is : 10
```

### if...else 语句

**if** 语句后面可以跟一个可选的 **else** 语句，当布尔表达式为假时执行。

#### 语法

C 编程语言中 **if...else** 语句的语法是：

```c
if(boolean_expression)
{
    /* statement(s) will execute if the boolean expression is true */
}
else
{
    /* statement(s) will execute if the boolean expression is false */
}
```

如果布尔表达式求值为**真**，则执行 **if 块**，否则执行 **else 块**。

C 编程语言将任何**非零**和**非空**值视为**真**，如果它是**零**或**空**，则视为**假**值。

#### 流程图

![](img/6e49c39a6ef9e32d938b03dc613e44f6_56_0.png)

### if...else if...else 语句

- 一旦某个 else if 成功，其余的 else if 或 else 将不再进行测试。

#### 语法

C 编程语言中 **if...else if...else** 语句的语法是：

```c
if(boolean_expression 1)
{
    /* Executes when the boolean expression 1 is true */
}
else if( boolean_expression 2)
{
    /* Executes when the boolean expression 2 is true */
}
else if( boolean_expression 3)
{
    /* Executes when the boolean expression 3 is true */
}
else
{
    /* executes when the none of the above condition is true */
}
```

#### 示例

```c
#include <stdio.h>

int main ()
{
    /* local variable definition */
    int a = 100;

    /* check the boolean condition */
    if( a == 10 )
    {
        /* if condition is true then print the following */
        printf("Value of a is 10\n");
    }
    else if( a == 20 )
    {
        /* if else if condition is true */
        printf("Value of a is 20\n");
    }
    else if( a == 30 )
    {
        /* if else if condition is true  */
        printf("Value of a is 30\n");
    }
    else
    {
        /* if none of the conditions is true */
        printf("None of the values is matching\n");
    }
    printf("Exact value of a is: %d\n", a );

    return 0;
}
```

当上述代码被编译并执行时，它产生以下结果：

```text
None of the values is matching
Exact value of a is: 100
```

### 嵌套 if 语句

在 C 编程中，**嵌套** if-else 语句始终是合法的，这意味着您可以在另一个 if 或 else if 语句中使用一个 if 或 else if 语句。

#### 语法

**嵌套 if** 语句的语法如下：

```c
if( boolean_expression 1)
{
    /* Executes when the boolean expression 1 is true */
    if(boolean_expression 2)
    {
        /* Executes when the boolean expression 2 is true */
    }
}
```

您可以以与嵌套 *if* 语句类似的方式嵌套 **else if...else**。

#### 示例

```c
#include <stdio.h>

int main ()
{
    /* local variable definition */
    int a = 100;
    int b = 200;

    /* check the boolean condition */
    if( a == 100 )
    {
        /* if condition is true then check the following */
        if( b == 200 )
        {
            /* if condition is true then print the following */
            printf("Value of a is 100 and b is 200\n" );
        }
    }
    printf("Exact value of a is : %d\n", a );
    printf("Exact value of b is : %d\n", b );

    return 0;
}
```

当上述代码被编译并执行时，它产生以下结果：

```text
Value of a is 100 and b is 200
Exact value of a is : 100
Exact value of b is : 200
```

### switch 语句

**switch** 语句允许一个变量与一组值进行相等性测试。每个值称为一个 case，被测试的变量会对每个 **switch case** 进行检查。

#### 语法

C 编程语言中 **switch** 语句的语法如下：

```c
switch(expression){
    case constant-expression :
        statement(s);
        break; /* optional */

    case constant-expression :
        statement(s);
        break; /* optional */

    /* you can have any number of case statements */
    default : /* Optional */
        statement(s);
}
```

以下规则适用于 **switch** 语句：

- 用于 **switch** 语句的 **表达式** 必须具有整型或枚举类型，或者是一个类类型，且该类具有到整型或枚举类型的单一转换函数。
- 在 switch 中可以有任意数量的 case 语句。每个 case 后跟要比较的值和一个冒号。
- case 的 **常量表达式** 必须与 switch 中的变量具有相同的数据类型，并且必须是常量或字面量。
- 当被测试的变量等于某个 case 时，该 case 之后的语句将一直执行到遇到 **break** 语句。
- 当遇到 **break** 语句时，switch 终止，控制流将跳转到 switch 语句之后的下一行。

