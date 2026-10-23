```
int addOne(int i){
    return ++i;
} /* return value plus one */
```

The argument, however, remains unchanged. For example, if the function is called as

```
int main(){
    int k=0;
    addOne(k);  /* k remains unchanged */
```

then the value of 'k' remains zero. This is because 'k' is passed to the function by value (or by name). In other words, when the function is called with 'k' as a concrete argument, a local integer variable, named 'i', is defined and initialized to the same value as 'k'. During the course of the function, it is only 'i' that changes, not 'k'.

The concrete argument can be changed only when it is passed by its address rather than by its value:

```
int addOne(int *q){
    return ++(*q);
} /* add one */
```

```
int main(){
    int k=0;
    addOne(&k);  /* k is indeed incremented by one */
```

This way, the "addOne" function takes an argument of type pointer-to-integer rather than integer. When called, the function increments the contents of this pointer by one, with a real effect that remains after the function has terminated.

In the call "addOne(&k)", the address of 'k' is passed as a concrete argument. The function then creates a local variable of type pointer-to-integer, named 'q', which is initialized with the address of 'k'. Then, 'k' is incremented through its address in 'q'. Although 'q' is destroyed when the function terminates, the effect on 'k' remains valid, as required.

# 1.16 I/O

So far, we have used the standard "printf" function, which prints a string of characters to the screen. In the code below, we also use the standard "scanf" function, which reads a string of characters from the screen. The first argument of the "scanf" function is this string: the rest of the arguments are the addresses of the variables in which the numbers in the string are placed. These arguments must be passed by address, so that they store the values that are read into them:

```
#include<stdio.h>
#include<stdlib.h>
int main(){
    int i=0;
    double x=0.;
    scanf("%d %f\n",&i,&x);
    printf("i=%d, x=%f\n",i,x);
```