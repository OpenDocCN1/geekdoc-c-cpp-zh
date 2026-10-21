

![](img/ad5299318df8d4d7c6df5eaa86590ea3_116_0.png)

Figure 3.42. Output screen of program.

EXPLANATION : Initially numbers of elements are taken is n. The first number is taken outside the loop and assumed to be maximum; this number is stored in max. Then remaining numbers are taken inside the loop. On each iteration the number is compared with the max, if the max is less than number taken then number will be the maximum one. This is checked through if statement. In the end when control comes out from while loop max is displayed.

## Break Statement

Break statement is used to come out early from loop without waiting for the condition to become false. We have seen one such usage of break in the switch-case statements. When the break statement is encountered in the while loop or any of the loops which will see later, the control immediately transfers to first statement out of the loop i.e., loop is exited prematurely. If there is nesting of loops the break will exit only from the current loop containing it.

Let’s write some programs which make use of break statement.

```
/*PROG 3.42 DEMO OF BREAK STATEMENT*/

#include <iostream.h>
void main()
{
    int x =1;
    while(x <= 5)
    {
    if(x == 3)
    break;
    cout << "Inside the loop x=" << x << endl;
    x ++;
    }
    cout << "Outside the loopx=" << x << endl;
}
```

> OUTPUT :
> Inside the loop x = 1
> Inside the loop x = 2
> Inside the loop x = 3

![](img/ad5299318df8d4d7c6df5eaa86590ea3_117_0.png)

### Figure 3.43. Output screen of program.

When x is 3 if condition becomes true, the body of the if statement is single break statement so all the statement in the loop following the break are skipped and control is transferred to the first statement after the loop which is printf which prints outside the loop x = 3.

```
/*PROG 3.43 TO CHECK WHETHER THE NUMBER IS PRIME OR NOT*/
#include <iostream.h>
void main()
{
int num,flag=0,c=2;
cout << "Enter the number\n";
cin >> num;
while(c < num/2)
{
if(num%c == 0)
{
flag = 1;
break;
}
c ++;
}
if(!flag)
cout << "Number is prime\n";
else
cout << "Number is not prime\n";
}
```

> OUTPUT :
> Enter the number
> 17
> Number is prime

![](img/ad5299318df8d4d7c6df5eaa86590ea3_118_0.png)

> Figure 3.44. Output screen of program.

A number is prime if it completely divisible by 1 and itself e.g., 1, 3, 5, 7, 11, 13, 17, 19, 23 etc. To check whether a number is prime or not we start from a counter c=2(every number divides by 1) continues till c<=num/2 since no number is completely divisible by a number which is more than half of that number. For example, 12 is not divisible by 7, 8, 9, 10, 11 which are more than 6. So we check if the number is divisible by any number<=num/2 then it cannot not be prime so if c%2==0 is true control sets flag =1 and come out from the loop. The flag was initialized to 0 in the beginning so if c%2==0 is true control sets flag =1 which means number is not prime else flag remains zero which means control never transferred to if block i.e., number is prime. So outside the loop we check this value of flag and prints accordingly.

## The Continue Statement

The continue statement causes the remainder of the statements following the continue to be skipped and continue with the next iteration of the loop. So, we can use continue statement to bypass certain number of statements in the loop on the basis of some condition given by if generally.

The syntax of continue statement is simply

```
continue;
```

Lets write a program to illustrate continue statement.

```
/*PROG 3.44 DEMO OF CONTINUE STATEMENT*/
#include <iostream.h>
void main()
{
int t=0;
while(t <= 10)
{
t ++;
if(t%2)
continue;
cout << "t=" << t << endl;
}
}
```

# OUTPUT :

- t = 2
- t = 4
- t = 6
- t = 8
- t = 10

![](img/ad5299318df8d4d7c6df5eaa86590ea3_119_0.png)

Figure 3.45. Output screen of program.

# EXPLANATION : When t is an odd number continue in the body of if condition causes loop to continue with next iteration of loop skipping printf statement. If number is even the number is simply printed as continue itself is skipped.

## 3.7.2 The For Loop

This is the second loops which are going to examine in this section. The for loop is most frequently used by programmers just because of its simplicity. The syntax of for loop is given here :

```
for (initialization; condition; increment/decrement)
{
    Statements;
    Statements;
    ...........;
}
```

There are various other syntaxes of for loop which we will see in a short while.

# /*PROG 3.45 DEMO OF FOR LOOP VER 1*/

```
#include <iostream.h>
void main()
{
    int t;
    for(t=1;t<=5;t++)
    cout << "t=" << t << endl;
}
```

OUTPUT :
 t = 1
 t = 2
 t = 3
 t = 4
 t = 5
 t = 6
 t = 7
 t = 8
 t = 9
 t = 10

![](img/ad5299318df8d4d7c6df5eaa86590ea3_120_0.png)

Figure 3.46. Output screen of program.

EXPLANATION : The first part of for loop t =1 is the initialization i.e., we are providing an initial value of 1 loop counter t. Next statement t<=10 is the testing condition for which this loop runs if condition is true. The last part is increment of loop works by first making t = 1 and then checking the condition whether t<=10 if so it executes the next statement following for i.e., printf. Recall as there is no braces after for loop only first statement is considered the body of the for loop. It hen goes to the increment the value of t, checks the test condition and executes the printf. This continues till the condition t<=10 is true. As soon as the condition becomes false in this case t =11 control comes out from loop and program terminates.

There are various syntaxes of writing for loop see the next few programs.

```
/*PROG 3.46 FOR LOOP SYNTAX-1 VER 1*/

#include <iostream.h>
void main()
{
    int t;
```

```
t = 10;
for(;t <= 100;t += 10)
cout << " " << t;
}
OUTPUT :
10 20 30 40 50 60 70 80 90 100
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_121_0.png)

Figure 3.47. Output screen of program.

EXPLANATION : In this program we have left the initialization part and have put this before the for loop, still semicolon (;) is must in the for loop.

The general syntax for such type of for loop as given in the above program is given below :

```
for (; condition; increment/decrement)
{
    Statements;
}
```

```
/* PROG 3.47 FOR LOOP SYNTAX2 VER 2*/

#include <iostream.h>
void main()
{
int t;
for(t=1;t <= 10;)
{
cout << " " << t;
t++;
}
}
OUTPUT :
1 2 3 4 5 6 7 8 9 10
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_122_0.png)

Figure 3.48. Output screen of program 3.47.

EXPLANATION : In this program we have written within braces. Note braces are must because you are having two statements which we want to make as body of the for loop.

The general syntax is given as :

```
for (initialization; condition;)
{
    Statements;
    Increment/decrement;
}
```

```
/*PROG 3.48 FOR LOOP SYNTAX3 VER 2*/

#include <iostream.h>
void main()
{
    int t;
    for(t=1;t<=10;)
    cout<<" "<<t;
    t++;
}
OUTPUT :
1 1 1 1 1 1 1 1 1 1 1...................(INFINITE TIMES)
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_122_1.png)

Figure 3.49. Output screen of program.

EXPLANATION : As there is no braces after the for loop only first statement is assumed as body of the for loop and t++ is not considered as part of the for loop so t<=10 remains true forever, result is infinite loop.

# Object-Oriented Programming C++ Simplified

```
/*PROG 3.49 FOR LOOP SYNTAX-4 VER*/
#include <iostream.h>
void main()
{
int t;
for(t=1;t<=10;)
cout << " " << t++;
}

OUTPUT :

1 2 3 4 5 6 7 8 9 10
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_123_0.png)

EXPLANATION : Here the mistake done in the above program has been removed. After printing the value of t it will be incremented (due to post increment). for loop works fine and prints 1 to 10.

```
/*PROG 3.50 FOR LOOP SYNTAX-3 VER 1*/
#include <iostream.h>
void main()
{
int t;
t = 1;
for(t<=10;)
cout << "t: " << t++ << endl;
}

OUTPUT :

t: 1 t: 2 t: 3 t: 4 t: 5 t: 6 t: 7 t: 8 t: 9 t: 10
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_123_1.png)

EXPLANATION : In this program we have left both unitization and increment/decrement part, still semicolon is necessary on both sides. The general syntax is :

