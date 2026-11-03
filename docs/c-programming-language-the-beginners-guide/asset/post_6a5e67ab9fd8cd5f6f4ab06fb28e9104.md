
```
    4 {
    5   puts("Pea green soup!"); 6 }
    7
```

- int main()
- void soup(void);

```
    10 {
```

- printf("For breakfast I had ");
- soup();
- printf("For lunch I had ");
- soup();

```
    15
    16 return(0);
    17 }
    18
    19
```

Save and build the code. On most computers, you’ll see one warning. Your compiler may report the misdeeds in a different manner. Either way, it is not good. You have to add the prototype. Go ahead and move *void soup(void)* above the main

```
    1 #include <stdio.h>
    3
    4 {
    5   puts("Pea green soup!"); 6 }
    7
```

```
```c
8 void soup(void);
soup(void);
soup(void); soup(void); soup(void); soup(void); soup(void);

soup(void);
soup(void); soup(void); soup(void); soup(void); soup(void);
soup(void);
soup(void);
```
```

Now, there are no and the output is the same as it originally was. Take a look at the code below:

```
```c
1 #include <stdio.h>
  3 void cheers(void); 4
  5 int main()
  6 {
```
```

- puts("Everyone gets free dinner!");
- cheers();
- puts("Everyone gets free dessert!");
- cheers();
- puts("Everyone pays higher taxes!"); 12

```
```c
13 return(0);
14 }
```
```

```
15
16 void cheers(void);
17 {
18 int x;
19
20 for(x=0;x<3;x++)
23 }
24
25
```

- printf("Huzzah! ");
- putchar('\n');

In this code, the cheers function contains its own at line 18. This variable is used only in the function here, to repeat the string three times. Build and run the code. You cannot reference variable x outside of its function. To prove it, insert a line above line 11 that displays its value.

```
1 #include <stdio.h>
3 void cheers(void); 4
5 int main()
6 {
```

- puts("Everyone gets free dinner!");
- cheers();
- puts("Everyone gets free dessert!");
- cheers();
- printf("%d\n", x);

```
puts("Everyone pays higher taxes!"); 13
14 return(0);
15 }
16
```

```
17 void cheers(void);
18 {
19 int x;
20
21 for(x=0;x<3;x++)
```

- printf("Huzzah! ");
- putchar('\n');

```
24 }
25
26
```

Save the change and build. Don't even bother trying to run it because you won't be able to. The compiler is basically saying, "What the heck is Now, try to define x and set its value inside the main function.

```
1 #include <stdio.h>
3 void cheers(void); 4
5 int main()
6 {
7 int x;
8
9 x=21;
```

- puts("Everyone gets free dinner!");

- cheers();
- puts("Everyone gets free dessert!");
- cheers();
- printf("%d\n", x);
- puts("Everyone pays higher taxes!"); 16

```
    17 return(0);
    18 }
    19
    20 void cheers(void);
    21 {
    22 int x;
    23
    24 for(x=0;x<3;x++)
```

- printf("Huzzah! ");
- putchar('\n');

```
    27 }
    28
    29
```

Now save, build and run the code. The value of *x* in the main function is unaffected by the *x* variable in the *cheers* function. They are considered as two different variables. Here’s another thing to remember: A function ends its run when its last statement is executed. In the *cheers* function, that’s a *putchar* at line 26.

You can bail out of a function early by using the *return* keyword. Type *return;* at line 26.

```
~~~c
1 #include <stdio.h>
3 void cheers(void); 4
5 int main()
6 {
7 int x;

8
9 x=21;

• puts("Everyone gets free dinner!");
• cheers();
• puts("Everyone gets free dessert!");
• cheers();
• printf("%d\n", x);

• puts("Everyone pays higher taxes!"); 16
17 return(0);
18 }
19
20 void cheers(void);
21 {
22 int x;
23
24 for(x=0;x<3;x++)

• printf("Huzzah! ");
~~~
```

- return;
- putchar('\n');

```
```
28 }
29
30
```
```

You don’t need to specify a value here because the *cheers* function is a *void* function—it doesn’t return anything. In the main function, *return* must specify a value as it does at line 17, because *main* is an *int* function. Save the changes, and then build and run the code.

The output is messy because the *putchar* statement is skipped. That code is never executed because of the *return* statement right above it. More often you’ll see a function return early based on a condition, which usually involves an *if* statement or a loop. Otherwise, anywhere the *return* is found marks the spot where the function bails out, and control returns to the calling function. Or, in the case of the main function, control is returned back to the operating system.

A function has got to it is that I/O thing again. Sure, a void function is necessary and obviously valid, but most functions chew an input, and do something based on that input.

In this section, we’ll talk about how functions can deal with arguments or values passed to the function. You’ll see how to declare such a function, how it deals with values, and how to pass more than a single value to a function. The code below contains the repeat function, which accepts one argument—an integer.

```
```
1 #include <stdio.h>
```
```

```
```c
3  void repeat(int count); 4
5  int main()
6  {

•  puts("At first the raven was like:");
•  repeat(1);
•  puts("But then he was all:");
•  repeat(5);

11
12 return(0);

13 }
14
15 void repeat(int count)
16 {
17 int x;
18

•  for(x=0;x
•  puts("Nevermore!");

21 }
22
23
```
```

Within the function, the integer variable is named. The function is called at lines 8 and 10, each time with a different argument. Inside the function, a local variable *x* is declared. It is used in the *for* statement, along with the *count* variable. Build and run the code.

The function can also accept integer variables as arguments. Make these modifications to the code:

- In the main function, declare integer variables *a* and *b*.
- Assign the value 1 to *a* and 5 to *b*.
- Use *a* and *b* in the two *repeat* functions.

```
```c
#include <stdio.h>

void repeat(int count);

int main()
{
    int a, b;

    a = 1;
    b = 5;

    puts("At first the raven was like:");
    repeat(a);
    puts("But then he was all:");
    repeat(b);

    return(0);
}

void repeat(int count)
```

```
16 void product(float a, float b, float c) 17 {
18 float p;
19
20 p = a * b * c;
21 printf("%f * %f *%f = %f\n",a,b,c,p); 22 }
23
```

In this code, you see a function that accepts three arguments. In this case, three floating-point values. The scanf function at line 10 reads in the three values. This is possible providing you format the input to match the format string. In the product function, the product of the three values is calculated and displayed. Build and run the code.

There is no limit to the number of arguments a function can accept. Although the more arguments, the more likely it will be to mess up the format. Functions don't necessarily need to eat all the same argument type either. Take a look at the code below:

```
1 #include <stdio.h>
3 void bar(char c, int count); 4
5 int main()
6 {
7 int x;
8
9 for(x=1;x<11;x++)
```

```
```c
10  bar('*',x*2);
11
12  return(0);
13 }
14
15 void bar(char c, int count)
16 {
17 int x;
18

•   for(x=0;x
•   putchar(c);
•   putchar('\n');

22 }
23
24
```
```

The *bar* function accepts two arguments: a character and an integer value. Build and run the code. The

*bar* function uses both of its arguments to output a bar of a certain character across the display.

Most functions in the C library return a value. Even when that value isn’t used, it’s available. Returning a value allows functions to generate output. Most of the time, that output is based on the input or arguments passed to the function. In this section, we’ll explain how functions return values. They can simply generate the information, or they can manipulate arguments to produce specific output.

We’ll also cover a few rules and regulations regarding functions in the C language. The code below contains a function called It’s a character function returning a `char` value. The function has no input according to its prototype at line 3.

```
```c
1 #include <stdio.h>
3 char gimmeAnA(void); 4
5 int main()
6 {
7 char grade;
8

• grade = gimmeAnA();

• printf("On this test your received an %c.\n",grade); 11
12 return(0);
13 }
14
15 char gimmeAnA(void)

16 {
17 return('A');
18 }
19
```
