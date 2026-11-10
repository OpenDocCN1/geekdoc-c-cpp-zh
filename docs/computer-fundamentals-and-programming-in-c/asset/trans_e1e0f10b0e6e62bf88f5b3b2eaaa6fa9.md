
“循环控制测试表达式在何时检查？”do-while 循环被认为是后测试循环，因为测试表达式位于循环体之后以及 while 关键字之后。即使测试表达式求值为假，do-while 循环也保证至少执行一次。

对于 while 语句，布尔表达式在循环体执行之前被检查。如果测试表达式求值为假，则循环体根本不会执行。

> **注意**
>
> - 对于 do-while 语句，先执行循环体，然后在循环体执行之后检查测试表达式。因此，do-while 语句始终至少执行一次循环体。

## 示例

- 26. 欧拉数 e 用作自然对数的底数。它可以使用以下公式近似计算：

  e = 1/0! + 1/1! + 1/2! + 1/3! + ... + 1/(n-1)! + 1/n!

  其中 n 足够大。编写一个程序，使用一个循环来近似计算 e，该循环在 e 的连续两个值之差小于 0.000001 时终止。

  ```c
  #include <stdio.h>
  int main()
  {
      double term = 1.0;
      double sum = 1.0;
      int n = 0;
      while (term >= 0.000001)
      {
          n++;
          term = term/n;
          sum = sum + term;
      }
      printf("\n Approximate value of e is: %lf ",sum);
      return 0;
  }
  ```

## 检查你的进度

- 1. 下面的 while 循环将重复多少次，即会打印多少个 x？

  ```c
  int i = 5; while(i-- > 0) printf("x");
  ```

  输出 5

- 2. 下面的代码会打印多少个 x？

  ```c
  int i = 5;
  while(i-- > 0)
      printf("x");
  printf("x");
  ```

  输出 6

- 3. 下面的 do-while 循环会打印什么？

  ```c
  int i = 0; char c = '0';
  do {
      putchar(c + i);
      ++i;
  } while(i < 5);
  ```

  输出 01234

- 4.

  ```c
  int main()
  {
      float s=1.0;
      int a=4;
      while(a<=10)
      {
          s = a*1.2;
          printf("%f",s);
      }
      return 0;
  }
  ```

  输出：由于 'a' 始终为 4，因此永远不会结束，这是一个无限循环！

- 5. 以下程序的输出将是什么？

  ```c
  #define infiniteLoop while(1)
  int main()
  {
      infiniteLoop;
      printf("DONE");
      return 0;
  }
  ```

  输出 无输出

  解释：main 中的 infiniteLoop 以 ';' 结尾。因此循环不会结束；并且“无输出”也不会打印。

## 10.6 应该使用哪种循环？

必须提出的一个问题是：为什么会有 while、do-while 和 for 循环？这是风格问题吗？

while 和 for 结构是前测试循环，而 do-while 结构是后测试循环。while 和 do-while 循环是事件控制的，而 for 循环是计数器控制的。当事先知道循环将执行多少次时，适合使用 for 循环。当事先不知道循环应在何时终止时，使用 while 和 do-while 循环。当可能不希望循环体执行哪怕一次时，使用 while 循环；当希望循环体至少执行一次时，使用 do-while 循环。这些标准有些随意，关于应使用哪种类型的循环并没有硬性规定。

> **注意**
>
> 使用循环时，始终要问以下问题：
>
> - 在什么条件下循环体将被执行？
> - 在什么条件下循环将终止？
> - 当循环停止时，循环控制变量的值是什么？

以下小节将讨论程序中控制重复的一些方法。有三种方式：哨兵值、预读和计数器。

### 10.6.1 使用哨兵值

哨兵值不是某个特定问题的合法数据值，但它是一种合适类型，用于检查“停止”值。它就像一个标志或指示器。有时必须允许程序用户输入他们想要输入的任意多关于某事物的信息。当用户完成所有信息输入后，用户可以输入一个哨兵值，让程序知道用户已完成信息输入。

### 示例

- 27. `-1` 可以用作哨兵值。

  ```c
  int main()
  {
      int age;
      printf("\n Enter an age(-1 to stop ):");
      scanf("%d",&age);
      while(age != -1)
      {
          ;
          printf("\n Enter an age(-1 to stop ):");
          scanf("%d",&age);
      }
      return 0;
  }
  ```

- 28. `-99` 也可以用作哨兵值。读取一组测试分数并计算它们的平均值。分数输入为 -99 表示用户的数据结束。

  ```c
  #include <stdio.h>
  int main()
  {
      int n, sum, score;
      float average;
      sum = 0;
      n = 0;
      printf("\n Enter a test score(-99 to quit):");
      scanf("%d", &score);
      while(score != -99)
      {
          sum += score;
          n++;
          printf("\n Enter a test score(-99 to quit):");
          scanf("%d",&score);
      }
      average = (float)sum / n;
      printf("\n The average is %f", average);
      return 0;
  }
  ```

### 10.6.2 使用预读

另一种控制重复的方法是使用预读。预读和哨兵值通常相伴使用。预读是在循环语句之前进行的数据输入，它允许输入第一个实际数据值，以便可以在循环语句中对其进行检查。由用户输入并由循环中的表达式测试的变量就是预读；预读的值就是所谓的哨兵值[参见第 10.6.1 节]。

### 示例

- 29. `age` 用作预读。

  ```c
  #include <stdio.h>
  int main()
  {
      int age;
      printf("\n Enter an age(-1 to stop):");
      scanf("%d",&age);
      while(age != -1)
      {
          .
          .
          .
          printf("\n Enter an age(-1 to stop):");
          scanf("%d",&age);
      }
      .
      .
      .
      return 0;
  }
  ```

- 30. `score` 用作预读。读取一组测试分数并计算它们的平均值。分数输入为 -99 表示用户的数据结束。

  ```c
  #include <stdio.h>

  int main()
  {
      int n, sum, score;
      float average;

      sum = 0;
      n = 0;

      printf("\n Enter a test score(-99 to quit):");
      scanf("%d", &score);
      while(score != -99)
      {
          sum += score;
          n++;
          printf("\n Enter a test score(-99 to quit):");
          scanf("%d", &score);
      }
      average = (float)sum / n;
      printf("\n The average is %f", average);
      return 0;
  }
  ```

EOF 也可以用于预读。考虑以下程序。

```c
#include <stdio.h>
#include <stdlib.h>
int main()
{
    int n, sum, score;
    float average;
    sum = 0;
    n = 0;
    printf("\n Enter test scores one by one(EOF to quit): ");

    while(scanf("%d", &score) != EOF)
    {
        sum += score;
        n++;
    }
    average = (float)sum / n;
    printf("\n The average is %f", average);
    return 0;
}
```

### 10.6.3 使用计数器

在程序执行期间控制重复的又一种方法是使用计数器。使用计数器需要知道某事物需要重复的确切次数。例如，如果必须指示程序用户输入十个数字，可以将计数器变量设置为 0，然后设置一个循环，在计数器的值小于十时继续循环（该循环将等于十次循环：0、1、2、...、9）。

### 示例

- 31. 编写一段代码，输出从 1 到 10 的数字。

  ```c
  #include <stdio.h>
  int main()
  {
      int count;
      count = 0;
      int numTimesNeeded = 10;
      while(count < numTimesNeeded)
      {
          printf("\n%d", (count + 1));
          count++;
      }
      return 0;
  }
  ```

- 32. 编写一段代码，允许用户输入十个测试分数，以求出这些分数的平均值。

  ```c
  #include <stdio.h>
  int main()
  {
      int count, score;
      float average;
      count = 0;
      int numTimesNeeded = 10;
      int total = 0;
      while(count < numTimesNeeded)
      {
          printf("\n Enter a test score");
          scanf("%d", &score);
          total += score;
          count++;
      }
      average = (float)total / numTimesNeeded;
      printf("\n The average is %f", average);
      return 0;
  }
  ```
