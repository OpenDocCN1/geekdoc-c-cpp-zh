
## 表 8：运算符的优先级与结合性

| 运算符 | 用途 | 优先级 | 结合性 |
| :--- | :--- | :--- | :--- |
| `>=` | 大于等于 | | |
| `==` | 等于 | 第七级 | 从左到右 |
| `!=` | 不等于 | | |
| `&` | 按位与 | 第八级 | 从左到右 |
| `^` | 按位异或 | 第九级 | 从左到右 |
| `\|` | 按位或 | 第十级 | 从左到右 |
| `&&` | 逻辑与 | 第十一级 | 从左到右 |
| `\|\|` | 逻辑或 | 第十二级 | 从左到右 |
| `? :` | 条件运算符 | 第十三级 | 从右到左 |
| `=, *=, -=, &=, +=, ^=, \|=, <<=, >>=` | 赋值运算符 | 第十四级 | 从右到左 |
| `,` | 逗号运算符 | 第十五级 | 从左到右 |

优先级和结合性的主要作用是帮助 C 语言编译器评估表达式。下一节将讨论 C 语言中表达式是如何被求值的。

### 5.3 C 语言中的表达式求值

到目前为止，我们讨论的重点是 C 语言中可用的不同运算符及其在表达式中的用法。如果语句没有正确构成，表达式的求值是一个主要问题。考虑表达式：`result = first * second + third / fourth – fifth`。在上面的表达式中，首先会执行标识符 `first` 和 `second` 的乘法运算，并将其值存储在一个临时位置。然后 `third` 将被 `fourth` 除，其值存储在另一个临时位置。然后，两个临时位置中的值将被相加，最后减去 `fifth`。图 10 展示了该表达式的求值顺序：

![](img/5d422ba7108ffdf64376be51eaf0c459_112_0.png)

从图 10 可以看出，如果两个相同优先级的运算符出现在表达式中，它们将根据其结合性（在本例中为从左到右）进行求值。为了改变求值顺序，我们可以使用括号。如果我们重写表达式为 `result = first + second * (third − fourth) / fifth`；那么标识符 `third` 和 `fourth` 将首先被相减，得到中间结果 1。中间结果 1 然后与 `second` 相乘，得到中间结果 2。中间结果 2 然后被 `fifth` 除。最后，与 `first` 相加。图 11 展示了新表达式的求值顺序：

![](img/5d422ba7108ffdf64376be51eaf0c459_113_0.png)

程序 12 说明了 C 语言中表达式是如何被求值的：

#### 程序 12

```c
/* Program to illustrate the evaluation of expression */

#include <stdio.h>
/* Beginning of main function */
main()
{
/* Declaration and initialization of unsigned integer variables */
unsigned int u_first = 25, u_second = 5, u_third = 15;
unsigned int u_fourth = 10, u_fifth = 12, u_result;
/* Expression without brackets */
u_result = u_first * u_second + u_third / u_fourth - u_fifth;
printf("Result of evaluation without using brackets = %d", u_result);
/* Expression with brackets */

u_result = u_first + u_second * (u_third - u_fourth) / u_fifth;
printf("\n Result of evaluation using brackets = %d \n", u_result);
return;
} /* End of function main */
```

**输出：**

Result of evaluation without using brackets = 114
Result of evaluation using brackets = 27

从程序 12 中可以观察到，当使用括号来控制求值时，同一表达式的输出会发生巨大变化。C 语言中使用的表达式被称为 C 语句。下一节将简要介绍 C 语言中可用的语句类别。

### 5.4 C 语言中的语句

由操作数和运算符组成的表达式被转换为 C 语句。生成的语句可能是可执行语句，也可能不是。在 C 程序中，可执行语句会引发某些动作，而不可执行语句则充当注释。C 语言提供了六种语句类别，如图 12 所示：

![](img/5d422ba7108ffdf64376be51eaf0c459_114_0.png)

▲ 图 12：C 语句的类别

程序 9 使用了表达式、复合语句、选择语句和迭代语句。这些语句的图示表示如图 13 所示：

![](img/5d422ba7108ffdf64376be51eaf0c459_114_1.png)

▲ 图 13：C 语句示例

从图 13 可以看出，C 程序中的表达式是一个可执行语句。通常，通过将表达式以分号 (;) 结尾来将其转换为 C 语句。分号向编译器指示语句的结束。所有以分号结尾的 C 语句都是可执行的。一组由零个或多个语句组合在一起，并用花括号包围，称为复合语句。所有 C 程序都由复合语句组成；一旦我们将 C 程序代码片段封闭在 `{ }` 内，它就成为一个复合语句。复合语句不以分号结尾。如果我们在结尾处用分号终止复合语句，编译器在编译时将会产生错误。

选择语句是指根据两个表达式的关系比较结果，决定执行哪个语句或哪一组语句的语句。迭代语句指的是允许重复执行代码片段的语句。关于带标签语句、跳转语句、选择语句和迭代语句的详细讨论将在后续章节中进行。

## 摘要

在本章中，我们学习了 C 语言中可用的不同运算符，如算术运算符、赋值运算符、关系运算符、增量/减量运算符、条件运算符、逻辑运算符、按位运算符和特殊运算符。我们还看到了如何对整数、实数和混合数值执行算术运算。在使用运算符时，我们学习了如何使用运算符和操作数形成不同类型的表达式，如一元、二元和单元表达式。然后讨论了决定哪个运算符先被评估的优先级，以及当遇到相同优先级的运算符时决定如何评估表达式的结合性。最后，我们查看了 C 语句的不同类别及其形成。

## 复习题

- Q1. 赋值运算符在 C 语言中的意义是什么？
- Q2. 类型转换在 C 语言中的意义是什么？
- Q3. 逗号运算符的用途是什么？
- Q4. 简写运算符的用途是什么？
- Q5. 列出并解释 C 语言语句的类别。
- Q6. 运算符优先级的意义是什么？
- Q7. 结合性优先级的意义是什么？
- Q8. 区分以下各项：
  - 一元运算符和二元运算符
  - 整数算术和实数算术
  - 除法运算符和取模运算符
  - 逻辑运算符和按位运算符
  - 增量运算符和减量运算符
- Q9. 给出以下程序的输出：

  i.
  ```c
  main()
  {
  int i_first = 10 & 20;
  printf("Result = %d",i_first);
  return;
  }
  ```

  ii.
  ```c
  main()
  {
      int i_num1 = 15, i_num2 = 10;
      int i_result;
      i_result = i_num1 | i_num2;
      printf("i_result = %d",i_result);
      return;
  }
  ```

  iii.
  ```c
  main()
  {
      i_num1 = 45, i_num2 = 15;
      float f_result;
      f_result = i_num1 / i_num2;
      printf("f_result = %f",f_result);
      return;
  }
  ```

  iv.
  ```c
  main()
  {
      i_num1 = 98, i_num2 = 75;
      int i_result;
      i_result = (i_num1 < 3) / (i_num2 > 2);
      printf("i_result = %x",i_result);
      return;
  }
  ```

  v.
  ```c
  main()
  {
      int i_first = 15, i_second = 25;
      int i_result;
      i_first += i_second;
      i_result = i_first++ ;
      printf("i_first = %d",i_first);
      printf("\ni_second = %d",i_second);
      printf("\ni_result = %d",i_result);
      return;
  }
  ```

  vi.
  ```c
  main()
  {
  double d_num = 15/5.5 + 99 * 2;
  printf("d_num = %ld",d_num);
  return;
  }
  ```

  vii.
  ```c
  main()
  {
      float f_num1 = 19.75, f_num2 = 5.75;
      float f_result;
      f_result = f_num1 % f_num2;
      printf("f_result = %f",f_result);
      return;
  }
  ```

  viii.
  ```c
  main()
  {
      i_num1 = 98, i_num2 = 75;
      printf("i_num1 = %d", i_num1 << 3);
      printf("i_num1 = %d", i_num2 >> 2);
      return;
  }
  ```

  ix.
  ```c
  main()
  {
      i_num1 = 700000, i_num2 = 70;
      int i_result;
      printf("i_result = %d",
             i_num1/i_num2);
      return;
  }
  ```

  x.
  ```c
  main()
  {
      int i_first = 55, int i_second = 35;
      int i_result;
      i_first -= i_second;
      i_result = i_second-- + ++i_first;
      printf("i_first = %d",i_first);
      printf("\ni_second = %d",i_second);
      printf("\ni_result = %d",i_result);
      return;
  }
  ```

