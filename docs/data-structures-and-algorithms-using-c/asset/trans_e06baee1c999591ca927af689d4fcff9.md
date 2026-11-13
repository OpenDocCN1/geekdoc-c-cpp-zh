

![](img/30fc9e3f8ee01facfae8d1c9621936b3_264_0.png)

现在，我们有能力为超过两个盘子的汉诺塔设计算法。我们将盘子堆栈分为两部分。最大的盘子（第 n<sup>th</sup> 个盘子）在其中一部分，而所有其他 (n-1) 个盘子在第二部分。

我们的最终目标是将盘子 **n** 从源移动到目标，然后将所有其他 (n-1) 个盘子放在其上。我们可以想象以递归的方式对所有给定的盘子集应用相同的操作。

遵循的步骤如下 –

- 步骤 1 – 将 n-1 个盘子从 **源** 移动到 **辅助**
- 步骤 2 – 将第 n<sup>th</sup> 个盘子从 **源** 移动到 **目标**
- 步骤 3 – 将 n-1 个盘子从 **辅助** 移动到 **目标**

汉诺塔的递归算法可推导如下 –

```
START
Procedure Hanoi(disk, source, dest, aux)
IF disk == 0, THEN
move disk from source to dest
ELSE
Hanoi(disk - 1, source, aux, dest) // Step 1
move disk from source to dest // Step 2
Hanoi(disk - 1, aux, dest, source) // Step 3
END IF
END Procedure STOP
```

要查看 C 语言编程中的实现，请单击此处。

## C 语言中的汉诺塔

### 程序

```
#include <stdio.h>
#include <stdbool.h>
#define MAX 10
int list[MAX] = {1,8,4,6,0,3,5,2,7,9};
void display(){ int i;
printf("[");
// navigate through all items
for(i = 0; i < MAX; i++){ printf("%d ",list[i]); }
printf("]\n"); }
void bubbleSort() {
int temp;
int i,j;
bool swapped = false;
// loop through all numbers
for(i = 0; i < MAX-1; i++) { swapped = false;
// loop through numbers falling ahead
for(j = 0; j < MAX-1-i; j++) {
printf("Items compared: [%d, %d] ", list[j],list[j+1]);
// check if next number is lesser than current no // swap the numbers.
// (Bubble up the highest number)
if(list[j] > list[j+1]) { temp = list[j];
list[j] = list[j+1]; list[j+1] = temp;
swapped = true;
printf("=> swapped [%d, %d]\n",list[j],list[j+1]);
}else {
printf("=> not swapped\n");
}
}
// if no number was swapped that means // array is sorted now, break the loop.
if(!swapped) {
break;
}
printf("Iteration %d#: ",(i+1)); display();
}
}
main(){
printf("Input Array: "); display();
printf("\n");
bubbleSort();
printf("\nOutput Array: "); display();
}
```

如果编译并运行上面的程序，将产生以下结果 –
输入数组：[1 8 4 6 0 3 5 2 7 9 ]

比较的项目：[ 1, 8 ] => 未交换
比较的项目：[ 8, 4 ] => 已交换 [4, 8]
比较的项目：[ 8, 6 ] => 已交换 [6, 8]
比较的项目：[ 8, 0 ] => 已交换 [0, 8]
比较的项目：[ 8, 3 ] => 已交换 [3, 8]
比较的项目：[ 8, 5 ] => 已交换 [5, 8]
比较的项目：[ 8, 2 ] => 已交换 [2, 8]
比较的项目：[ 8, 7 ] => 已交换 [7, 8]
比较的项目：[ 8, 9 ] => 未交换

迭代 1#：[1 4 6 0 3 5 2 7 8 9 ]
比较的项目：[ 1, 4 ] => 未交换
比较的项目：[ 4, 6 ] => 未交换
比较的项目：[ 6, 0 ] => 已交换 [0, 6]
比较的项目：[ 6, 3 ] => 已交换 [3, 6]
比较的项目：[ 6, 5 ] => 已交换 [5, 6]
比较的项目：[ 6, 2 ] => 已交换 [2, 6]
比较的项目：[ 6, 7 ] => 未交换
比较的项目：[ 7, 8 ] => 未交换

迭代 2#：[1 4 0 3 5 2 6 7 8 9 ]
比较的项目：[ 1, 4 ] => 未交换
比较的项目：[ 4, 0 ] => 已交换 [0, 4]
比较的项目：[ 4, 3 ] => 已交换 [3, 4]
比较的项目：[ 4, 5 ] => 未交换
比较的项目：[ 5, 2 ] => 已交换 [2, 5]
比较的项目：[ 5, 6 ] => 未交换
比较的项目：[ 6, 7 ] => 未交换

迭代 3#：[1 0 3 4 2 5 6 7 8 9 ]
比较的项目：[ 1, 0 ] => 已交换 [0, 1]
比较的项目：[ 1, 3 ] => 未交换
比较的项目：[ 3, 4 ] => 未交换
比较的项目：[ 4, 2 ] => 已交换 [2, 4]
比较的项目：[ 4, 5 ] => 未交换
比较的项目：[ 5, 6 ] => 未交换

迭代 4#：[0 1 3 2 4 5 6 7 8 9 ]
比较的项目：[ 0, 1 ] => 未交换
比较的项目：[ 1, 3 ] => 未交换
比较的项目：[ 3, 2 ] => 已交换 [2, 3]
比较的项目：[ 3, 4 ] => 未交换
比较的项目：[ 4, 5 ] => 未交换

迭代 5#：[0 1 2 3 4 5 6 7 8 9 ]
比较的项目：[ 0, 1 ] => 未交换
比较的项目：[ 1, 2 ] => 未交换
比较的项目：[ 2, 3 ] => 未交换
比较的项目：[ 3, 4 ] => 未交换

输出数组：[0 1 2 3 4 5 6 7 8 9 ]

## 38. 斐波那契系列 数据结构与算法

斐波那契系列通过将前两个数字相加来生成后续数字。斐波那契系列从两个数字开始 – F₀ 和 F₁。F₀ 和 F₁ 的初始值可以分别取为 0, 1 或 1, 1。

斐波那契系列满足以下条件 – Fn = Fn-1 + Fn-2

因此，斐波那契系列可以是这样的 – F₈ = 0 1 1 2 3 5 8 13

或者，是这样的 –

F₈ = 1 1 2 3 5 8 13 21 为说明目的，F₈ 的斐波那契显示如下 –

![](img/30fc9e3f8ee01facfae8d1c9621936b3_267_0.png)

### 斐波那契迭代算法

首先，我们尝试起草斐波那契系列的迭代算法。

```
Procedure Fibonacci(n)
declare f0, f1, fib, loop
set f0 to 0 set f1 to 1
display f0, f1
for loop <- 1 to n
fib <- f0 + f1 f0 <- f1
f1 <- fib
display fib end for
end procedure
```

要了解上述算法在 C 语言编程语言中的实现，请单击此处。

### C 语言中的斐波那契交互程序

### C 语言中的斐波那契程序 RecursionDemo.c

```
#include <stdio.h>
int factorial(int n) {/base case
if(n == 0){
return 1;
return n * factorial(n-1); }
}
int fibbonacci(int n){
if(n == 0){
return 0;
}else if(n == 1){
return 1;
}else {
return (fibbonacci(n-1) + fibbonacci(n-2));
}
}
main(){
int n = 5; int i;
printf("Factorial of %d: %d\n" , n , factorial(n)); printf("Fibbonacci of %d: " ,n);
for(i = 0;i<n;i++){
printf("%d ",fibbonacci(i));
}
}
```

如果编译并运行上面的程序，将产生以下结果 –

5 的阶乘：120
5 的斐波那契：0 1 1 2 3

### 斐波那契递归算法

让我们学习如何创建斐波那契系列的递归算法。递归的基准条件。

START
Procedure Fibonacci(n)
declare f0, f1, fib, loop
set f0 to 0 set f1 to 1
display f0, f1
for loop <- 1 to n
fib <- f0 + f1 f0 <- f1
f1 <- fib
display fib end for
END

要了解上述算法在 C 语言编程语言中的实现，请单击此处。

### C 语言中的斐波那契递归程序

### C 语言中的斐波那契程序

```
#include <stdio.h>
int factorial(int n) {//base case
if(n == 0){
return 1;
return n * factorial(n-1); }
}
int fibbonacci(int n){
if(n == 0){
return 0;
}else if(n == 1){
return 1;
}else {
return (fibbonacci(n-1) + fibbonacci(n-2));
}
}
main(){
int n = 5; int i;
printf("Factorial of %d: %d\n" , n , factorial(n)); printf("Fibbonacci of %d: " ,n);
for(i = 0;i<n;i++){
printf("%d ",fibbonacci(i));
}
}
```

如果编译并运行上面的程序，将产生以下结果 –

5 的阶乘：120

5 的斐波那契：0 1 1 2 3

