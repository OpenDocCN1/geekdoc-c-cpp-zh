![](bbox=[0.24, 0.09, 0.53, 0.25])

**FIGURE 4.5** The *while* construct

# 4.5.7 The *for* construct

The *for* construct is another loop structure supported by the C language. It is more flexible than the while construct. Hence, the for construct is often a preferred choice. The syntax of a *for* construct is as follows:

```
for (e1; e2; e3) {
    s;
}
```

where e1, e2, and e3 are C expressions and ‘s’ represents one or more valid C statements. Figure 4.6 shows the flowchart for the *for* loop.

In Figure 4.6, the expression e1 is evaluated first. The expression e2 is then evaluated; if it is false the loop terminates. Otherwise, ‘s’ representing one or more C statements will be executed. The expressions e3, and e2 are then evaluated, and the process continues. The expression e1 normally contains code to initialize the loop. The expression e2 describes the exit condition. The purpose of the expression e3 is to modify such as increment the initialized value of expression e1. This will be the exit condition so that the loop terminates at some point.

For example, assume e1 as k = 4, e2 as k<8, and e3 as k = k + 1 in Figure 4.7. With the above data, the “for” loop can be written as

: for (k = 4; k<8; k = k + 1)

In this “for” loop, ‘k’ is initialized with 4. Since, 4 is less than 8, the condition is true and hence, the statement(‘s’) within the curly brackets will be executed. ‘k’ is then incremented to 5. The loop then goes back to e2 to check the condition. The loop will be repeated until k = 7. This can be illustrated by the following C-program:

```
#include <stdio.h>
int k;
main () {
    for (k = 4; k<8; k = k+ 1){
        printf (“k= %d\n”, k);
    }
}
```

After compilation and execution of the above C-program, the following result will be generated:

```
k = 4
k = 5
k = 6
k = 7
```