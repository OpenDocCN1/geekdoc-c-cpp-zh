C takes the approach that it is better to package the parts of a general conditional loop rather than invent a proper enumeration loop. The C for loop, and it would be better called a conditional loop, is:

```
```c
for(initial set up; test if loop should continue; update test condition){
    body of loop
}
```
```

When you write a C for loop the compiler uses the expressions to construct a conditional loop. For example:

```
```c
for(i = 0; i < 10; i++){
    printf("%d\n", i);
}
```
```

is equivalent to the previous conditional loop:

```
```c
int i = 0;
loopStart:
    if (i >= 10) goto loopEnd;
    printf("%d\n", i);
    i++;
    goto loopStart;
loopEnd:
    printf("end of loop");
```
```

The i = 0 is performed before the loop starts, the i < 10 is evaluated at the start of the loop and the body of the loop only executes if it is true and the i++ is performed at the end of the loop before the next potential repeat. Notice that the condition in the for loop has to be true for the loop to continue. In the example conditional loop the condition has to be true for the loop to end but this is a minor difference.

In this form the C for loop is perfectly OK as an enumeration loop. All C programmers learn this form as an idiom and read it as a loop that repeats for i from 0 to 9. It is as if the C for loop is frozen in a restricted but useful form:

```
```c
for(index=startvalue; index=endvalue; index++){
}
```
```

and the only things you ever change are the startvalue and endvalue and the loop repeats for index from the startvalue to one less than the endvalue. In this form it really is an easy to use enumeration loop. From here most C programmers learn to vary it slightly to get different effects.