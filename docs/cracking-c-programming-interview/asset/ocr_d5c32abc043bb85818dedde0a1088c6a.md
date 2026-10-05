# 59. d

Explanation: The variable assignment is the step as the previous question, there is only a change in step (iv), here's p = p+3.

```
p = p+3;
(iv) p = 3;
p = p3;
p = 500;
#step size is 4 (pointer)
#p=512;
```

```
--> (****)2;
--> (*ptr[1]+b'a';
--> (**512)+2;
--> (*ptr+1))b'a';
--> 4000/2;
--> (*500+1))98-97;
--> (*504) + 1;
/step size is 1
String at address 4002 will
returned by prnt using
%,
O/p: cat
--> 3000/1; step
String at address 3001 will
returned by prnt using %.
O/p: ove
```

![](bbox=[0.433, 0.259, 0.513, 0.305])

# 60. c

Explanation: When a user requests a dynamic memory allocation, the C program requests memory. If the memory is available, the memory manager component of the operating system allocates the memory to the program. If the system is too busy, the memory manager can deny the request to allocate memory for the program. Here, in a given program the memory is allocating dynamically in an infinite loop without deallocating(free()). When the main memory (RAM) gets completely allocated to our program. There is no memory left for other processes, the heap gets overflow and the system (having Unix type operating system) hangs.

If we deallocate the memory in each iteration, the heap will not overflow, the system will not hang, just the hello 10 will get printed infinite time. See the following program:

```
#include<stdio.h>
#include<stdlib.h>
int main() {
while (1) {
int *p = (int *)malloc(sizeof(int));
*p=10;
printf("hello %d", *p););
```