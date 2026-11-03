
The semi-colon doesn’t follow the *for* statement’s parenthesis. Instead, the semi-colon follows a single looping statement, which is shown at line 8, or a series of statements are enclosed in curly brackets. Build and run the code. The values 0 through 9 are output. This is actually typical for a C loop. In C programming, you start counting at 0, not 1. Humans start counting at 1. To fix the loop for the human’s eyes, change the *printf* statement at line 8 to read like so:

```c
1  #include <stdio.h>
2
3  int main()
4  {
5  int x;
6
7  for(x=0;x<10;x++)
8  printf("%d\n",x+1);
9
10 return(0);
11 }
12
13
```

This modification doesn’t change the value, only the output. Save, build and run the code.

## The Nested Loop

The one thing that's great with a *for* loop is that you can make use of the concept of a nested loop. This is easier than using a *while* loop in C language. In this section, we'll talk about how to make a nested loop, as well as how to avoid the common looping pitfalls that programmers encounter in the C language.

Take a look at the code below:

```text
       _______

_______  _______
_______  _______
_______  _______
_______

_______  _______  _______
_______  _______  _______  _______

       _______
```

The sample code that we have outputs ten randomly selected numbers. Build and run this code. As you can see from the output, there's now a row of ten randomly selected values. The spacing that's present in between each value is attained by making use of the tab character `\t`, which is at line 14 of the code.

Now, let's go ahead and try to make a 100 value grid. In addition to the single row of ten values that we already have, we need to create nine more rows of ten values. To accomplish this task, most C programmers use the nested loop, or a secondary *for* loop that repeats the output ten more times. Take a look at the code below:

![](img/7d7500a0ed1507e3351945dfe5a0440d_128_0.png)

The code above is a modified version of the code that we used earlier. It now has an extra loop. The column loop, which was the old loop, is now nested within a new loop called the row loop. The indentation that you see in the code is for readability—it helps match up the curly brackets of each statement. Build and run this code. As you can see, you now have a grid of 100 randomly selected values. Take a look at the code below:

```c
    1 #include <stdio.h>
    2
    3 int main()
    4 {
    5     int alpha, numeric;
    6
    7
    8     for(alpha='A';alpha<'K';alpha++)
    9     {
    10        for(numeric=0;numeric<10;numeric++)
    11            printf("%c%d\t",alpha,numeric);
    12        putchar('\n');
    13    }
    14
    15    return(0);
    16 }
    17
    18
```

The nested loop that you see above might be a little bit easier to read. The outer alpha loop sweeps through letters A through K is the limit. The inner loop loops from 0 to 9. You'll also notice that this inner loop does not make use of any curly brackets since it only contains one statement. At line 11, the loop variables are displayed. Build and run this code.

You can better observe how the nested loops execute in the output. First, the outer loop executes. Then, the inner loop outputs the values 0 through 9. It is then followed by the loop which also outputs 0 through 9, and so forth. Take a look at the code below:

```c
1  #include <stdio.h>
2
3  int main()
4  {
5  char ch, t;
6
7  printf("Type a letter ‘a’ to ‘z’: ");
8  scanf("%c",&ch);
9
10 for(t='a';t<='z';t++)
11 {
12 putchar(t);
13 }
14 putchar('\n');
15
16 return(0);
17 }
18
19
```

Input is prompted and then the alphabet is displayed. What we'd like you to think about doing is how to stop the loop when the letter input is equal to variable t in the loop. You don't need to change the four statements to make that happen. Instead, you need to put statements within the loop that would bust out of the loop when the character is input.

The key is to use an if test and follow that with a break statement. Take a look at the solution below:

```c
1 #include <stdio.h>
2
3 int main()
4 {
5 char ch, t;
6
7 printf("Type a letter ‘a’ to ‘z’: ");
8 scanf("%c",&ch);
9
10 for(t='a';t<='z';t++)
11 {
12 putchar(t);
13 if( t == ch )
14 break;
15 }
16 putchar('\n');
```

At line 13, add *if (t == ch)* and then *break*. If you don’t put the two equal signs in there, what you get is an assignment. In C, assignments always evaluate true. Don’t forget about the semicolon after the break statement. Save, build and run the code.

Remember to check these two items in a *for* statement: the looping condition and the iteration. If either is off, the loop would go on forever. The compiler doesn’t check for flaws in logic. That’s your job. A good tip is to read the *for* statement. Set *t* equal to character; while *t* is less than or equal to character, increment.

If you change the condition to just *t='z'* for example, it would evaluate true and the loop would run forever. So watch your conditions and your iterations.

## Chapter 8: Anatomy of a Function

The C library is brimming with functions. These functions do a lot of things, but perhaps not everything you need for your programs. Therefore, when necessary, you can concoct your own C language functions. In fact, most programmers have dozens, if not hundreds of their own functions.

In this chapter, we introduce you to the function. You’ll see how to setup and prototype a function, how to call or access the function, and how to bail out of a function early. Like everything in the C language, a function has a certain style, and various etiquettes must be followed to add a function to your code.

A function has a type, a name, and arguments in parenthesis. A *type* is a value returned by the function—its output. The *name* is a unique name that identifies the function. The *arguments* are zero, one, or more values passed to the function—its input. Below, the alpha function has no input or output, which is valid in the C language. Therefore, it is a void function.

`void alpha(void)`

Void is a variable type, which means “I have no variable type.” Function count is an integer function. It generates or returns integer values. It requires no input, and therefore has no arguments.

`int count(void)`

Function hangUp returns no values, so it’s a void function. It does, however, accept a single character as input. The character is an argument. It is referenced by a variable. Before you can use a function, it must be introduced to the compiler. That way the compiler can check the function by checking the prototype. Also, the prototype is a statement. It ends in a semi-colon.

Line 8 calls the function. It has no arguments, so the parenthesis is empty. The function itself is found at line 14. This is effectively a repeat of the prototype minus the semi-colon. The statements belonging to the function are enclosed in curly brackets. Now build and run the code.

To call the function again, you simply specify it again. Duplicate line 8 to line 9.

```c
1 #include <stdio.h>
2
3 void blorf(void);
4
5 int main ()
6 {
7     puts("The main () function always runs first");
8     blorf();
9     blorf();
10    puts("Thanks, blorf()");
11
12    return(0);
13 }
14
```

Save, build and run the code. As you can see, the output appears twice. The prototype works like a definition for the function, describing how to use it before it appears in the code. You can avoid specifying a prototype, but only when you write the function before it is used. To see an example, take a look at the code below:

```c
1 #include <stdio.h>
2
3 void soup(void)
4 {
5 puts("Pea green soup!");
6 }
7
8 int main()
9 {
10 printf("For breakfast I had ");
11 soup();
12 printf("For lunch I had ");
13 ");
14 ");
```

The *soup* function appears above the *main* function. That's okay because the compiler still sees them in a function, and it is always the first function that is executed in the program. What is missing here is the prototype for the *soup* function. Build and run the code.

As you can see, the code outputs text as expected. But try this: move the *soup* function after the *main* function like so:

```c
1 #include <stdio.h>
2
3
```
