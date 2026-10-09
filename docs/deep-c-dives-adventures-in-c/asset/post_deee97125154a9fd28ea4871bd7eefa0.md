
## C's General Conditional Loop

C takes the approach that it is better to package the parts of a general conditional loop rather than invent a proper enumeration loop. The C for loop, and it would be better called a conditional loop, is:

```c
for(initial set up; test if loop should continue; update test condition){
    body of loop
}
```

When you write a C for loop the compiler uses the expressions to construct a conditional loop. For example:

```c
for(i = 0; i < 10; i++){
    printf("%d\n", i);
}
```

is equivalent to the previous conditional loop:

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

The `i = 0` is performed before the loop starts, the `i < 10` is evaluated at the start of the loop and the body of the loop only executes if it is true and the `i++` is performed at the end of the loop before the next potential repeat. Notice that the condition in the for loop has to be true for the loop to continue. In the example conditional loop the condition has to be true for the loop to end but this is a minor difference.

In this form the C for loop is perfectly OK as an enumeration loop. All C programmers learn this form as an idiom and read it as a loop that repeats for i from 0 to 9. It is as if the C for loop is frozen in a restricted but useful form:

```c
for(index=startvalue; index=endvalue; index++){
}
```

and the only things you ever change are the `startvalue` and `endvalue` and the loop repeats for index from the `startvalue` to one less than the `endvalue`. In this form it really is an easy to use enumeration loop. From here most C programmers learn to vary it slightly to get different effects.

For example:

```c
for(index = startvalue; index <= endvalue; index++){
}
```

gives an enumeration loop that runs from `startvalue` to, and including, `endvalue`, whereas:

```c
for(index = startvalue; index >= endvalue; index--){
}
```

gives an enumeration loop that runs from `startvalue` down to `endvalue` assuming `startvalue > endvalue` and so on.

These idioms are what makes the C for loop usable for beginners and non-beginners alike. It is a for loop with direct mapping to the underlying assembly language that it is compiled to and as such it is brilliant. But it has its evil side – it is too flexible.

### While and Until

The for loop is very general, but it is limited to having its exit point at the start of the loop. This makes it a while loop. Loops differ in where they place their exit points, i.e. where the test for the end of the loop is. This is another distinguishing feature in the loop zoo – loops differ in both the number of exit points they have and where they are placed. While loops test at the start and until loops test at the end.

It should be clear that the difference is that a while loop can exit without ever executing the body of the loop, but an until loop has to execute the body of the loop before making a test. You can summarize this as a while loop repeats 0 to *n* times and an until loop repeats 1 to *n* times. In other words, an until loop has to execute at least once.

C has a while loop, but it is entirely equivalent to a particular form of the for loop. The while loop:

```c
while(condition){
}
```

is exactly the same as:

```c
for(;condition;){
}
```

and, yes, you can leave out any part of the for loop as long as it makes sense. Indeed:

```c
for(;;)
```

is an infinite loop, often used in IoT applications and in constructing more general loops. It never ends because there is no condition specified.

C also has an until loop and this is one that is more difficult to convert into a for loop:

```c
do{
    body of loop
}while(condition);
```

If this is an until loop, why does it end with while?

The answer is that in a conventional until loop the condition is for the loop to end. In a conventional while loop the condition is for it to continue. You can see that `until = !while` in that until ends the loop and while continues it.

So even though the C until loop has its exit point at the end it uses a condition for it to continue – hence the use of while. It’s a historical accident caused by the desire to reuse the compiler’s handling of the while condition i.e. to avoid introducing an `until(condition)`.

You can convert this to a for loop, but only if you are prepared to repeat the body of the loop:

```c
body of loop
for(condition){
    body of loop;
}
```

## Break and Continue

What about loops that have their exit point not at the end and not at the beginning?

Before languages like C, loops could exit from any point in their body simply by using a jmp instruction to outside the loop. This was not a good idea because it relied on the programmer to keep things simple and clear. For a long time it was asserted that you only needed a for loop, a while loop and an until loop – and this is true. Any program that can be written, can be written using just these loops. This is the original premise of “structured programming”, the first attempt to make programming better.

Today we tend not to be as hardline and the break and continue statements were introduced in C90. The break statement is equivalent to a goto that jumps out of the loop, i.e. to the first instruction following the loop. The continue statement is equivalent to a goto that jumps to the start of the loop, i.e. it skips any remaining statements in the body of the loop.

Both constructs let you construct loops that complete a fractional number of repeats. For example:

```c
for(i = 0; i < 10; i++){
    print("before\n");
    if(i == 5) break;
    printf("after\n", i);
}
```

This loop executes the before 5 times, but the after 4 times and you can see that there is a sense in which it repeats the loop body four and a half times. You can write a completely general loop with any number of exit points anywhere in the loop using:

```c
for(;;){
    first part of loop
        if(condition) break;
    second part of loop
        if(condition) break;
    third part of loop
    and so on
}
```

## Find It and Fix It

If you are wondering what the break and continue statements are for, you have never encountered, or never thought about, the find it or fix it algorithms.

The find it algorithm is simply having to scan through an array to find a specified value. Many attempt to implement this as an enumeration loop because you know the length of the array n:

```c
for(i = 0; i < n; i++){
    if(array[i] == target) hit = i;
}
printf("%d\n",hit);
```

The problem is that the loop repeats n times, even if the target is in the first element. You can fix this inefficiency using the break statement:

```c
for(i = 0; i < n; i++){
    if(array[i] == target) break;
}
printf("%d\n",i);
```

This brings the loop to an end when the target is found but notice that it relies on the value of i not changing due to the operation of the break. This is the case unless you use the C99 idiom of declaring the index in the for statement:

```c
for(int i = 0; i < n; i++){
    if(array[i] == target) break;
}
printf("%d\n",i);
```

This doesn't work because i no longer exists at the end of the loop. It is also worth reminding the reader that a for loop is a block and as such variables declared within it only live for as long as the for loop is executing, see Dive 8.

In this case, however, the use of an enumeration loop isn't really justified. For a true enumeration loop you have to know the number of repeats before the loop begins. In this case we only know the maximum number of repeats is the number of elements in the array – the loop may finish earlier if the target is found. This is not an enumeration loop. It is a conditional loop where we know the maximum number of repeats and it can be written more expressively as:

```c
i = 0;
while (array[i] != target && i<n) {
    i++;
}
```

You can even write this loop as a C for loop:

```c
for(i = 0; array[i]!= target && i<n; i++){
}
printf("%d\n",i);
```

However, many programmers think that having a compound condition to keep a loop running is less clear than a misuse of a for loop at the cost of a break.

Finally what is the continue for?

The continue is for the “fix it” loop. If you need to scan through an array and pick out elements that need to be “fixed” or processed in some way you might use:

```c
for(i = 0; i < n; i++){
    if (array[i]!= fixFlag) continue;
    fix(array[i]);
}
```

If the array element needs fixing then it is fixed, otherwise the continue skips the fix and moves the loop on to the next element of the array.

This is an enumeration loop proper, as we know the number of repeats before the loop begins. However, we don't really need the continue and can write instead:

```c
for(i = 0; i < n; i++){
    if (array[i]== fixFlag) fix(array[i]);
}
```

The continue just gives you a way of skipping the last part of a loop and you can always do this with an if statement.
