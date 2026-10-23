# 1.21 Example: Arithmetic Expression

Here we use recursion in a program that reads an arbitrarily long arithmetic expression, prints it in the postfix and prefix formats, and calculates it. The postfix (respectively, prefix) format of a binary arithmetic expression puts the symbol of the arithmetic operation before (respectively, after) the arguments. For example, the arithmetic expression 2 + 3 has the postfix format +23 and the prefix format 23+. (No parentheses are used.)

The above tasks are carried out recursively as follows. The arithmetic expression is stored in a string or an array of digits and arithmetic symbols like '+', '-', etc. This string is fed as input into the function "fix()" that carries out the required task. In this function, the string is scanned in reverse order (from right to left). Once a character that corresponds to an arithmetic operation is found, the string is split into two substrings, and the function is called recursively for each of them (see Figure 1.7).

To implement this procedure, we need to define some elementary functions. We start with a function that copies the first 'n' characters from a string 's' to a string 't':

```
#include<stdio.h>
void copy(char* t, char* s, int n){
    for(int i=0;i<n;i++)
        t[i]=s[i];
    t[n]='\0';
} /* copy n first characters from s to t */
```

The function "fix()" defined below carries out one of three possible tasks: writing in postfix format, writing in prefix format, or computing the value of the arithmetic expression. The particular task that is carried out is determined by the value of its last argument, the integer named "task". The arithmetic expression is passed to the "fix()" function as its first argument, and its length is specified in the second argument. The third argument, the integer "task", takes three possible values that specify the required task: if it is zero, then the arithmetic expression is printed in the postfix form; if it is one, then the arithmetic expression is printed in the prefix form; and if it is two, then the arithmetic expression is calculated and its value is returned.

![](bbox=[0.22, 0.84, 0.82, 0.92])

Figure 1.7. The "fix()" function calculates 3·7 + 12/3 by scanning it backward until the '+' is found and splitting it into two subexpressions, 3·7 and 12/3, which are calculated recursively and added.