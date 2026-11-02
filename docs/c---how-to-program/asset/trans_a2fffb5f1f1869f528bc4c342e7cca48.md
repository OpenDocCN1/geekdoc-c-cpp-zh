

完整的第二次细化如图3.9所示。我们使用空行将 `while` 语句分隔开，以提高程序的可读性。

这段伪代码现在已足够细化，可以转换为C语言。对应的C程序及两次示例执行结果如图3.10所示。我们利用了C语言的一个特性，即允许在定义变量时进行初始化（第9–11行）。这种初始化发生在编译时期。另外请注意，当输出 `unsigned int` 类型的值时，需要使用 `%u` 转换说明符（第33–34行）。

```
1  Initialize passes to zero
2  Initialize failures to zero
3  Initialize student to one
4
5  While student counter is less than or equal to ten
6      Input the next exam result
7
8      If the student passed
9          Add one to passes
10     else
11         Add one to failures
12
13     Add one to student counter
14
15  Print the number of passes
16  Print the number of failures
17  If more than eight students passed
18     Print "Bonus to instructor!"
```

图 3.9 | 考试结果问题的伪代码。

![](img/d0d3b7423c2d9e5650be79209ea1885d_122_0.png)

> **软件工程观察 3.5**
> 
> *经验表明，在计算机上解决问题最困难的部分是为解决方案设计算法。一旦正确的算法被确定下来，生成一个可工作的C程序的过程通常就变得 straightforward（直截了当）了。*

![](img/d0d3b7423c2d9e5650be79209ea1885d_122_1.png)

> **软件工程观察 3.6**
> 
> *许多程序员编写程序时从不使用伪代码之类的程序开发工具。他们认为自己的最终目标是在计算机上解决问题，而编写伪代码只会推迟最终输出的产生。*

```
1 // Fig. 3.10: fig03_10.c
2 // Analysis of examination results.
3 #include <stdio.h>
4
```

图 3.10 | 考试结果分析。（共3部分，第1部分）

```
// function main begins program execution
int main( void )
{
   // initialize variables in definitions
   unsigned int passes = 0; // number of passes
   unsigned int failures = 0; // number of failures
   unsigned int student = 1; // student counter
   int result; // one exam result

   // process 10 students using counter-controlled loop
   while ( student <= 10 ) {

      // prompt user for input and obtain value from user
      printf( "%s", "Enter result (1=pass,2=fail): " );
      scanf( "%d", &result );

      // if result 1, increment passes
      if ( result == 1 ) {
         passes = passes + 1;
      } // end if
      else { // otherwise, increment failures
         failures = failures + 1;
      } // end else

      student = student + 1; // increment student counter
   } // end while

   // termination phase; display number of passes and failures
   printf( "Passed %u\n", passes );
   printf( "Failed %u\n", failures );

   // if more than eight students passed, print "Bonus to instructor!"
   if ( passes > 8 ) {
      puts( "Bonus to instructor!" );
   } // end if
} // end function main
```

```
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 2
Enter Result (1=pass,2=fail): 2
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 2
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 2
Passed 6
Failed 4
```

**图 3.10** | 考试结果分析。（共3部分，第2部分）

```
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 2
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Enter Result (1=pass,2=fail): 1
Passed 9
Failed 1
Bonus to instructor!
```

**图 3.10** | 考试结果分析。（共3部分，第3部分）

## 3.11 赋值运算符

C语言提供了几个赋值运算符，用于简化赋值表达式。例如，语句

```
c = c + 3;
```

可以使用加法赋值运算符 `+=` 缩写为：

```
c += 3;
```

`+=` 运算符将运算符**右侧**表达式的值加到运算符**左侧**变量的值上，并将结果存储在运算符左侧的变量中。任何形式为

```
variable = variable operator expression;
```

的语句，其中 *operator* 是二元运算符 +、-、*、/ 或 %（以及我们将在第10章讨论的其他运算符），都可以写成如下形式：

```
variable operator= expression;
```

因此，赋值语句 `c += 3` 将 3 加到 c 上。图3.11展示了算术赋值运算符、使用这些运算符的示例表达式及其解释。

| 赋值运算符 | 示例表达式 | 解释 | 赋值 |
|---|---|---|---|
| *假设：int c = 3, d = 5, e = 4, f = 6, g = 12;* |  |  |  |
| += | c += 7 | c = c + 7 | 将10赋给c |
| -= | d -= 4 | d = d - 4 | 将1赋给d |
| *= | e *= 5 | e = e * 5 | 将20赋给e |
| /= | f /= 3 | f = f / 3 | 将2赋给f |
| %= | g %= 9 | g = g % 9 | 将3赋给g |

**图 3.11** | 算术赋值运算符。

## 3.12 自增和自减运算符

C语言还提供了一元自增运算符 `++` 和一元自减运算符 `--`，其总结如图3.12所示。如果要将变量 c 加1，可以使用自增运算符 `++`，而不必写成 `c = c + 1` 或 `c += 1`。如果将自增或自减运算符放在变量之前（即前缀形式），它们分别称为前自增运算符或前自减运算符。如果将自增或自减运算符放在变量之后（即后缀形式），它们分别称为后自增运算符或后自减运算符。对变量进行前自增（前自减）会使变量先加1（减1），然后将其新值用于所在的表达式中。对变量进行后自增（后自减）会先将变量的当前值用于所在的表达式中，然后变量值再加1（减1）。

| 运算符 | 示例表达式 | 解释 |
| --- | --- | --- |
| `++` | `++a` | 将 a 加 1，然后使用 a 的新值于 a 所在的表达式中。 |
| `++` | `a++` | 使用 a 的当前值于 a 所在的表达式中，然后将 a 加 1。 |
| `--` | `--b` | 将 b 减 1，然后使用 b 的新值于 b 所在的表达式中。 |
| `--` | `b--` | 使用 b 的当前值于 b 所在的表达式中，然后将 b 减 1。 |

图 3.12 | 自增和自减运算符。

图3.13演示了 `++` 运算符的前自增和后自增版本之间的区别。对变量 c 进行后自增，会使其在 `printf` 语句中使用**之后**才被加1。对变量 c 进行前自增，会使其在 `printf` 语句中使用**之前**被加1。

```
1   // Fig. 3.13: fig03_13.c
2   // Preincrementing and postincrementing.
3   #include <stdio.h>
4
5   // function main begins program execution
6   int main( void )
7   {
8       int c; // define variable
9
10      // demonstrate postincrement
11      c = 5; // assign 5 to c
12      printf( "%d\n", c ); // print 5
13      printf( "%d\n", c++ ); // print 5 then postincrement
14      printf( "%d\n", c ); // print 6
```

图 3.13 | 前自增和后自增。（共2部分，第1部分）

```
15
16      // demonstrate preincrement
17      c = 5; // assign 5 to c
18      printf( "%d\n", c ); // print 5
19      printf( "%d\n", ++c ); // preincrement then print 6
20      printf( "%d\n", c ); // print 6
21   } // end function main
```

```
5
5
6

5
6
6
```

图 3.13 | 前自增和后自增。（共2部分，第2部分）

该程序显示了使用 `++` 运算符前后 c 的值。自减运算符（`--`）的工作方式类似。

## 良好编程实践 3.4

*一元运算符应直接紧邻其操作数，中间不要有空格。*

图3.10中的三条赋值语句

```
passes = passes + 1;
failures = failures + 1;
student = student + 1;
```

可以使用赋值运算符更简洁地写成：

```
passes += 1;
failures += 1;
student += 1;
```

也可以使用前自增运算符写成：

```
++passes;
++failures;
++student;
```

或者使用后自增运算符写成：

```
passes++;
failures++;
student++;
```

这里需要重点指出，当在一条语句中单独对变量进行自增或自减时，前自增形式和后自增形式的效果相同。只有当变量出现在更大的表达式中时，前自增与后自增才会产生不同的效果（前自减与后自减也是如此）。在我们目前研究过的表达式中，只有简单的变量名才能作为自增或自减运算符的操作数。

