
# FUNCTIONS

```c
#include<stdio.h>
#include<conio.h>
#include<math.h>
void numtochar(int);
void main() {
    int num;
    printf("................Number to String conversion........................\n\n\n
```

```c
    break;
    case 5 : printf("Five");
    break;
    case 6 : printf("Six");
    break;
    case 7 : printf("Seven");
    break;
    case 8 : printf("Eight");
    break;
    case 9 : printf("Nine");
    break;
```

```c
}temp=temp/10;
length1--;
}
```

## Program 5.3 Number to String conversion part II

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_93_0.png)

### Output 5.3 Output for Program 5.3

Type III Functions with arguments and return type
Program 5.4 explains the factorial problem, wherein the function factorial() takes an integer argument and returns an integer value.

```c
#include<stdio.h>
#include<conio.h>
int factorial(int);
void main() {
    int num, fact;
    printf("................Finding the FACTORIAL value................................\n\n");
    scanf("\nenter the number: %d",&num); // num is here
// actual parameter
    fact=factorial(num);
    printf("The factorial value is %d\n", fact);
    getch();
}
```

```c
int factorial(int num) {
    int i, f=1;
    for (i=1;i<=num;i++)
    f=f*i;
    return f;
}
```

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_93_1.png)

## Program 5.4 Program to find the factorial

On executing the Program 5.4, the user will be confronted with the following output screen Output 5.4.

### Finding the FACTORIAL value

```
enter the number:5
The factorial value is 120 
```

### Output 5.4 Output for Program 5.4

## 5.1.5. Library routines and functions

Referring to the benefits of functions in section 5.1, the third point speaks about the library functions. We can define some of the frequently used operations such as addition, subtraction, multiplication and put them all under one header file named arithmetic_operations.h, and, when needed, the header file should be included in the user program, so that the methods defined in the header files can be simply called without redefining them. Much like scan() and printf() without defining them. Program 5.5 would explain it even better.

```c
int add(int a, int b) {
    return a+b;
}
int sub(int a, int b) {
    if(b>a)
        return b-a;
    else
        return a-b;
}
int mul(int a, int b) {
    return a*b;
}
int div(int a, int b) {
    return a/b;
}
```

## HEADER FILE: arithmetic_operations.h

```c
#include<stdio.h>
#include<conio.h>
#include "arithmetic_operations.h"
void main() {
    int a,b;
    printf("enter the two values..\n");
    scanf("%d %d", &a, &b);
    printf("\na+b = %d\n", add(a,b)); //note: added for clarity
    printf("\na-b = %d\n", sub(a,b));
    printf("\na*b = %d\n", mul(a,b));
    printf("\na/b = %d\n", div(a,b));
    getch();
}
```

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_94_0.png)

## Program 5.5 Functions as Library Routines

On executing Program 5.5 with the values 36 and 6, the following output would appear!

```
enter the two values..
36
6
a+b : 42
a-b : 30
a*b : 216
a/b : 6
```

### Output 5.5 – Output of Program 5.5

## 5.1.6. Function calls and stack.

Let's look into more intrinsic details about the working of functions.

As previously mentioned, main() is the entry point for any program. The compiler executes line by line until a user defined function call is encountered. The compiler needs to jump to the location of function definition outside the main() if it encounters a function call inside the main(). If it doesn't find an appropriate function definition, it flashes an error! OK, What if it finds one? It executes line by line in the function definition until the function is terminated by a ')'.

After the brace closure '}', the compiler jumps back to the previous position in main(). This is the mechanism followed for function executions. One probable question at this place would be, how can compiler reclaim the place it jumped off? The answer to this question lies in a data structure called 'Stack'. It is much like a container where we put something in and take off. The basic operations in stack are:

- 1. Push – Putting the item to the stack.
- 2. Pop – Taking out the item from the stack.

Note: Stack operates in LIFO fashion (Last In First Out). TOS is a pointer which points to Top of the Stack. During the function call, we push local environment. While returning from the function, we pop and restore local environment. An example would make it simpler. Assume a call is performed from main() to user defined fun(). The following steps are performed during the function call:

- The compiler saves local environment of main() in the stack.
- Jumps to first instruction of fun(), and executes function.
- Then returns from fun(), restores environment of main().
- Resumes execution in main just after call.

As another example, f(1) calls f(2), f(2) in turn calls f(3). Where, f(3) is the innermost function, and gets first. After that, control returns to f2. Finally, f1 gets executed and the control returns to main. With this information the basics of stack, Jump to the next section. More stacks and function calls would be presented in Section 5.3 Recursion.

## 5.2. CALL BY VALUE CALL BY REFERENCE

A very interesting topic is 'call by value and reference'. So far, the reader would have come across many function calls, some of them had arguments, and some did. Those which had arguments actually passed the values of variables. For example, consider Program 5.3, where the function passed the value of actual parameter "num" to dummy variable "num". What actually happens while passing the value to function definition?

- A copy of the value is given to the function definition.
- The function definition deals with the copy of the original variable, and not the original value.
- Here is the knot. Any modification to the value inside function definition won't affect the original.
- The original will remain as such in the memory.

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_96_0.png)

Figure 5.1 Pass By Value

Program 5.6 would explain the concept more clearly.

```c
#include<stdio.h>
#include<conio.h>
void swap(int, int);
void main() {
    int a,b;
    printf("Enter the two numbers..\n");
    printf("a=%d"); scanf("%d",&a);
    printf("b=%d"); scanf("%d",&b);
    printf("\nBefore swapping, from main()...\n");
    printf("a=%d,b=%d",a,b);
    swap(a,b);
    printf("\nAfter swapping, from main()...\n");
    printf("a=%d,b=%d",a,b);
    getch();
}
void swap(int a, int b) {
    int c;
    c=b;
    b=a;
    a=c;
    printf("\nInside the function..After swapping..\n");
    printf("a=%d,b=%d",a,b);
}
```

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_97_0.png)

## Program 5.6 Swap using call value

```
Enter the two numbers..
a=895
b=1053
Before swapping, from main()...
a = 895,b = 1053
Inside the function..After swapping..

a = 1053,b = 895
After swapping, from main()...
a = 895,b = 1053
```

### Output 5.6 Output of Program 5.6

As Output 5.6 shows, the values of a and b remain the same before and after calling the swap. But inside the function it is evident that both the values get exchanged. But it doesn't get reflected inside the main(). This is the nature of "passing by value". Whatever we do for the dummy variables inside the function, there will be no change happening to the actual values! Refer Figure 5.2 for pictorial understanding. If we want the changes to get reflected inside the main(), using "pass by reference" would help!!

### Before Swap After Swap

| Local Variables in main() | | Local Variables in main() |
| --- | --- | --- |
| a | | a |
| 10 | | 10 |
| | swap(a,b); | |
| b | | b |
| 20 | | 20 |

| Local variables in function | void swap(int a, b) | Local variables in function |
| --- | --- | --- |
| a | | a |
| 10 | | 20 |
| b | | b |
| 20 | | 10 |

Figure 5.2 Pictorial representation of swap operation using call value
