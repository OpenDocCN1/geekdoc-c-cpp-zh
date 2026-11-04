**Problem H1.** Continuation to previous program (*PatternH1.c*), modify the program for the following situation.

In program (*PatternH1.c*), the count variable started with the value -1 given as :

```
```c
int count = -1;// counter to increment/decrement
```
```

Required to match the output (*PatternH1*) of the modified program (*PatternH1_2.c*) by making the following change:

```
```c
int count = 0;// counter to increment/decrement
```
```

This time program has to initialise the variable count with the value 0 instead of -1 and yet still it should give the correct matching output as that of pattern program (*PatternH1.c*).

# ### PatternH1_2.C

```
```c
#include <stdio.h>
int main() {
        int totalRows = 7;// number of rows to display
        int count = 0;// counter to increment/decrement .

        // Row level Repetitive Action :
        // Action1:Executes Column level Repetitive Action
        // Action2:Move cursor to next row.

        // Write your logic

        return 0;
}
```
```

# ### Output

```
```text
        *
      * * *
    * * * * *
  * * * * * * *
* * * * * * * * * *
* * * * * * * * * * * *
* * * * * * * * * * * * *
  * * * * * * * * * * *
    * * * * * * * *
      * * * * *
        * * *
          *
```
```