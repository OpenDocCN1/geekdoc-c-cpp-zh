**Takeaway:** A function using a structure as argument copies the entire structure. If the structure contains an array, it too will be copied.

**Caution:** A program may run out of memory when using structures as arguments. A structure containing numerous members and large arrays can lead to stack overflow and cause the program to abort.

# 14.8.1 `structure_in_func.c`: An Introductory Program

Program 14.7 uses two functions that use a three-member structure named `time` as an argument. The `display_structure` function simply outputs the values of the three members. The `time_to_seconds` function returns the time after conversion to seconds. Note that we have now moved the structure declaration before `main` and before the function declarations. `time` is now a global template even though its variable `t` is not global.

```
```c
/* structure_in_func.c: Use a structure as a function argument. */
#include <stdio.h>

struct time {                 /* Must be declared before main because ... */
    short hour;               /* ... following function declarations ... */
    short min;                /* ... use this structure. */
    short sec;
};

void display_structure(struct time f_time);
int time_to_seconds(struct time f_time);
int main(void)
{
    struct time t;
    fputs("Enter a time in hh:mm:ss format: ", stdout);
    scanf("%hhd:%hhd:%hhd", &t.hour, &t.min, &t.sec);
    display_structure(t);
    int value = time_to_seconds(t);
    printf("Value of t in seconds: %d\n", value);
    return 0;
}

void display_structure(struct time f_time)
{
    printf("Hours: %hd, Minutes: %hd, Seconds: %hd\n",
           f_time.hour, f_time.min, f_time.sec);
    return;
}

int time_to_seconds(struct time f_time)
{
    return f_time.hour * 60 * 60 + f_time.min * 60 + f_time.sec;
}
```
```

PROGRAM 14.7: **structure_in_func.c**