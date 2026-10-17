
有时我们需要基于多个条件进行多路选择。C 支持两种决策结构，即 `if-else` 梯子和 `switch`，它们允许多路选择。`if-else` 梯子是之前研究的 `if-else` 语句的一种变体，而 `switch` 具有其自身的结构。下一小节讨论了如何使用 `if-else` 梯子。

# If-Else 梯子语句

`if-else` 梯子更常被称为 `else-if` 梯子，因为它将 `else` 语句与另一个 `if` 关联。梯子通过将几个条件的 `else` 部分与 `if` 语句级联形成。梯子中的条件从上到下评估。一旦某个测试条件被评估为 `true`，其对应的动作块就会被执行。一旦 `true` 动作块执行完毕，整个 `if` 语句的执行就停止了。`else if` 梯子的语法如下：

```text
if( 测试条件 1 )
    动作语句 1;
else if( 测试条件 2 )
    动作语句 2;
:
:
else if (测试条件 n)
    动作语句 n;
else
    默认动作语句;
```

从上述语法中可以观察到，我们从 `if-else` 语句开始，然后每个 `else` 语句都附加了 `if` 语句。最后一个 `else` 语句成为默认动作语句。如果所有测试条件都评估为 `false`，则会执行默认动作语句。图 7 展示了 `else-if` 梯子的逻辑流程：

![](img/5d422ba7108ffdf64376be51eaf0c459_131_0.png)

如图 7 所示，每个测试条件在 `true` 动作块执行后都有一个出口点。这里的最坏情况是所有 `n` 个测试条件都失败。在这种情况下，编译器必须检查指定的所有测试条件。程序 8 说明了 `else-if` 梯子的使用：

#### 程序 8

```c
/*  用于说明 if-else 梯子使用的程序  */
#include <stdio.h>
/*  主函数开始  */
main()
{
    /*  声明变量  */
    float f_celsius;
    /*  输入数据  */
    printf("Enter temperature: ");
    scanf("%f", &f_celsius);

    /*  检查气候状况  */
    /*  根据状况打印适当信息  */
    if(f_celsius >= -40.0 && f_celsius < 10.0)
    {
        printf("It is the coldest period of year.\n");
    }
    else if(f_celsius >= 10.0 && f_celsius < 20.0)
    {
        printf("The weather is comfortable at present.\n");
    }
    else if(f_celsius >= 20.0 && f_celsius < 50.0)
    {
        printf("It is the hottest period of year.\n");
    }
    else
    {
        printf("Mankind cannot survive in this temperature.\n");
    }

    return;
}  /*  主函数结束  */
```

**输出 1：**

输入温度：-45

人类无法在这种温度下生存

**输出 2：**

输入温度：-5

这是一年中寒冷的时期

**输出 3：**

输入温度：15.25

目前天气舒适

**输出 4：**

输入温度：25

这是一年中炎热的时期

可以看出，在程序 8 中，我们输入一个摄氏温度。然后，该温度使用 `if-else` 语句与各种数值范围进行比较。一旦某个测试条件变为 `true`，信息将被打印，并且程序停止执行。

`if-else` 梯子确实为我们提供了多路选择。然而，随着选择数量的增加，程序的复杂性也会增加。为了使程序看起来更具可读性和紧凑性，C 提供了另一种称为 `switch` 的多路选择结构。下一小节讨论了如何使用 `switch` 结构。

#### Switch 语句

`if-else` 结构是一种派生机制，用于在 C 语言中实现多路选择。C 提供了一种内置的决策结构，称为 `switch`，用于多路选择。使用这种决策结构可以提高程序的可读性。完整的 `switch` 决策结构由四个 C 关键字组成，即 `switch`、`case`、`default` 和 `break`。`switch` 语句的语法如下：

```text
switch (表达式)
{
    case 值 1:
        [动作块 1]
        [break;]
    case 值 2:
        [ 动作块 2 ]
        [break;]
    case 值 3:
        [ 动作块 3 ]
        [break;]
    : 
    : 
    case 值 N:
        [动作块 N]
        [break;]
    [default:
        [默认动作块]
        [ break ;]
    ]
}
```

在上述语法中，我们注意到在许多地方使用了方括号。方括号表示其中的语句是可选的。紧跟在 `switch` 关键字后面的术语“表达式”指的是可以评估为整型常量或字符常量的表达式。每个 `case` 选项包含一个整型常量或字符常量，称为 `case` 标签。`case` 标签始终以冒号 (`:`) 结尾。

表达式的值在评估后，会与 `case` 关键字沿自上而下指定的值进行比较。当表达式值与 `case` 值匹配时，编译器开始执行 `switch` 结构中此 `case` 中提到的语句。为了退出 `switch` 结构中特定的 `case` 块，我们使用

**`break`** 关键字。当未找到匹配项时，编译器将执行在 **`default`** 动作块中定义的语句。图 8 展示了 `switch` 结构的逻辑流程：

![](img/5d422ba7108ffdf64376be51eaf0c459_134_0.png)

从图 8 中可以观察到，控制流程是从上到下的。为了阻止流程执行所有语句，我们使用关键字 `break`。如果在动作块末尾未使用 `break` 语句，编译器将继续执行后续动作块中的所有语句，直到找到 `break` 语句或遇到 `switch` 结构的末尾。此外，**`default`** 案例并不一定非要出现在所有动作块的末尾。它可以出现在 `switch` 结构中的任何位置。例如，它也可以是第一个案例，而 `switch` 结构仍会正常工作。程序 9 说明了 `switch` 结构的使用方法：

### 程序 9

```c
/* 程序用于说明 switch 结构的使用 */

#include <stdio.h>

/* main 函数开始 */
main()
{
/* 声明变量 */
int i_first, i_second;
int i_choice, i_result;

/* 输入数据 */
printf("Enter first number: ");
scanf("%d", &i_first);
printf("\nEnter second number: ");
scanf("%d", &i_second);

/* 打印菜单 */
printf("\n*****Operation Menu*****\n");
printf("Enter 1 to perform Addition.\n");
printf("Enter 2 to perform Subtraction.\n");
printf("Enter 3 to perform Multiplication.\n");
printf("Enter 4 to perform Division.\n\n");

/* 接受用户选择 */
printf("Enter your choice : ");
scanf("%d", &i_choice);

/* 检查输入的选择并执行所需的操作 */
/* switch 结构开始 */
switch(i_choice)
{
  case 1:
    i_result = i_first + i_second;
    printf("\nAddition of %d + %d is %d\n", i_first, i_second, i_result);
    break;
  case 2:
    i_result = i_first - i_second;
    printf("\nSubtraction of %d - %d is %d\n", i_first, i_second, i_result);
    break;
  case 3:
    i_result = i_first * i_second;
    printf("\nMultiplication of %d * %d is %d\n", i_first, i_second, i_result);
    break;
  case 4:
    if(i_second == 0)
      printf("\nDivision not possible\n");
    else
    {
      i_result = i_first / i_second;
      printf("\nDivision of %d / %d is %d\n", i_first, i_second, i_result);
    }
    break;
  default:
    printf("\nInvalid choice no operation possible.\n");
}  /* switch 结构结束 */
return;
}  /* main 函数结束 */
```

##### 输出 1：

```text
Enter first number: 10
Enter second number: 15
*****Operation Menu*****
Enter 1 to perform Addition.
Enter 2 to perform Subtraction.
Enter 3 to perform Multiplication.
Enter 4 to perform Division.

Enter your choice : 2

Subtraction of 10 - 15 is -5
```

##### 输出 2：

```text
Enter first number : 50

Enter second number : 0

*****Operation Menu*****
Enter 1 to perform Addition.
Enter 2 to perform Subtraction.
Enter 3 to perform Multiplication.
Enter 4 to perform Division.

Enter your choice : 4

Division not possible
```

##### 输出 3：

```text
Enter first number : 15

Enter second number : 25

*****Operation Menu*****
Enter 1 to perform Addition.
Enter 2 to perform Subtraction.
Enter 3 to perform Multiplication.
Enter 4 to perform Division.

Enter your choice : 5

Invalid choice no operation possible.
```

从程序 9 中可以观察到，`switch` 结构获取 `i_choice` 的值并将其与不同的案例值（如 1、2、3 和 4）进行比较。如果任何选择与指定的案例值匹配，则执行该案例块中提到的操作。请注意，在 `case 4` 中，我们使用了 `if-else` 语句。由于 `else` 语句包含多条需要执行的语句，我们为其提供了一个作用域。注意我们在 `default` 动作语句中未使用 `break` 语句。一旦 `default` 动作块执行完毕，下一条语句表示 `switch` 结构的末尾，流程将从 `switch` 结构的这一点自动向下移动。

让我们再看一个例子，以更好地理解 `switch` 结构的用法。程序 10 说明了 `switch` 结构的使用，其中 `default` 动作块被放置在开头。

### 程序 10

```c
/* 程序用于说明 switch 结构的使用 */
#include <stdio.h>
#include <ctype.h>

/* main 函数开始 */
main()
{
	/* 声明变量 */
	char c_character;

	/* 输入数据 */
	printf("Enter a character: ");
	scanf("%c", &c_character);

	/* 检查输入的字符并确定其类型 */

	/* switch 结构开始 */
	switch(c_character)
	{
	default:
		if(isdigit(c_character))
			printf("\nCharacter %c is number.\n", c_character);
		else if (isalpha(c_character))
			printf("\nCharacter %c is consonant.\n", c_character);
		else
			printf("\nCharacter %c is special character.\n", c_character);
		break;
	case 'A':
	case 'a':
	case 'E':
	case 'e':
	case 'I':
	case 'i':
	case 'O':
	case 'o':
	case 'U':
	case 'u':
		printf("\nCharacter %c is vowel\n", c_character);
	}	/* switch 结构结束 */
	return;
}	/* main 函数结束 */
```

##### 输出 1：

```text
Enter a character: e
Character e is vowel
```

##### 输出 2：

```text
Enter a character: 0
Character 0 is number
```

##### 输出 3：

```text
Enter a character: q
Character q is consonant
```

##### 输出 4：

```text
Enter a character: $
Character $ is special character
```

从程序 10 中可以观察到，`default` 语句被放置在 `switch` 结构的开头。`default` 动作块中的最后一条语句是 `break` 语句。这里的 `break` 语句是必须的，用于阻止编译器执行其他任何案例动作。此外，请注意，我们只为 `case 'A'`, `case 'a'`, `case 'E'`, `case 'e'`, `case 'I'`, `case 'i'`, `case 'O'`, `case 'o'`, `case 'U'`, 和 `case 'u'` 写了一个动作块。一旦其中任何案例匹配了 `c_character` 的值，执行控制权就会转移到语句 `printf("\nCharacter %c is vowel\n", c_character);`。注意，我们在上述案例的动作块之后没有写 `break` 语句。原因与程序 9 中指出的原因类似。

请注意，当编写 `switch` 案例时，案例标签不能重复。这意味着一个常量（整数或字符）只能作为案例标签出现一次。在程序 10 的情况下，`case 'A'` 和 `case 'a'` 指的是两个不同的标签，因为 `'A'` 和 `'a'` 的 ASCII 值不同。美国国家标准学会（ANSI）C 为我们提供了创建最多 257 个案例标签的规定。

因此，如果我们有多个选项可供选择，多路选择结构是很有用的。

### 总结

在本章中，我们学习了如何改变程序的执行流程。C 语言提供了决策结构，如 `if`、`if-else`、`嵌套 if`、`if-else` 梯子和 `switch case`，以改变执行流程。具体来说，`if`、`if-else` 和嵌套 `if` 决策结构用于双向选择。对于多路选择，我们使用 `if-else` 梯子和 `switch-case` 决策结构。我们还讨论了当 `if` 语句在程序中嵌套时出现的悬挂 `else` 问题。

### 复习题

- 1. **Q1.** C 语言中双向选择的意义是什么？

- 2. **Q2.** 解释 C 语言中用于实现双向选择的不同机制。

- 3. **Q3.** 举例说明编译器如何解决悬挂 `else` 问题。

- 4. **Q4.** 举例说明使用 `switch` 结构相对于 `if-then-else` 梯子的优势。

- 5. **Q5.** `break` 语句在 `switch` 结构中的意义是什么？

- 6. **Q6.** 区分双向选择和多路选择。

- 7. **Q7.** 判断以下陈述是正确还是错误：

  - i. 双向选择语句在 C 语言中使用简单的 `if` 语句实现。

  - ii. 不相关的 `if` 语句可以在 C 程序中用 `switch` 结构替换。

  - iii. 以 `if(1)` 开始的语句块总是会被执行。

  - iv. C 语言不允许嵌套 `if` 语句。

  - v. `switch` 结构的案例标签可以是浮点值。

  - vi. 关键字 `default` 在 `switch` 结构中总是最后一个案例。

**问题 8.** 如果有错误请修正并给出以下代码的输出：

i.

```c
main()
{
    float f_a = 0.5 , f_b = 0.7 ;
    if ( f_b < 0.7 )
        if ( f_a < 0.5 )
            printf("HELLO");
        else
            printf("BYE");
    else
        printf("HI");
}
```

ii.
