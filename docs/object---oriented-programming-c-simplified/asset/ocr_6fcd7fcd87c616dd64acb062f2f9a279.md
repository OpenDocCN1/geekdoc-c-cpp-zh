included. Now whether you input vowel in upper case or lower case it is passed to switch block in lower case which is checked ch for any of the five vowels.

# 3.6 UNCONDITIONAL BRANCHING USING GOTO

The goto statement is used to transfer control of program from one point to other. In fact it make program control to jump to the statement specified by a lable. This type of **unconditional transfer of control using goto is called branching.** The label must be in the same function in which **goto** is used. The general syntax for goto statement is as follows :

```
goto label;
```

We understand the use of **goto** using a program.

```
/*PROG 3.38 DEMO OF GOTO VER 1*/

#include <iostream.h>
#include <math.h>
void main()
{
int x;
start :
cout << "Entera +ve number\n";
cin >> x;
if(x < 0)
goto start;
cout << "sqrt of number is" << sqrt(x) << endl;
}
OUTPUT :
Entera +ve number
-30
Entera +ve number
40
sqrt of number is 6.32456
```

![](bbox=[0.33, 0.73, 0.67, 0.84])

Figure 3.39. Output screen of program.