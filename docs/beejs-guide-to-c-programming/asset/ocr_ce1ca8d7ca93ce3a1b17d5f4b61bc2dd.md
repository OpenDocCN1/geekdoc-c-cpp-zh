# Chapter 3. Variables and Statements

```
while (i < 10) {
 printf("is is %d\n", i);
 i++;
}
```

// Do the exact same thing with a for-loop:

```
for (i = 0; i < 10; i++) {
 printf("is is %d\n", i);
}
```

That's right, folks—they do the same thing. But you can see how the for statement is a little more compact and easy on the eyes (JavaScript users will fully appreciate its origins at this point)\It's split into three parts, by semicolons. The first is the initialization, the second is the loop condition, and the third is what would happen at the end of the loop if the loop condition is true. All of these parts are optional.

for (initialize); loop if this is true; do this after each loop

Note that the loop will not execute a single time if the loop condition starts off.

for-loop fun fact!

You can use the comma operator to do multiple things in each clause of the loop:

```
for (i = 0, j = 999; i < 10; i++, j--) {
 printf("%d, %d\n", i, j);
}
```

An empty for will run forever:

```
for(); { // "forever"
 printf("I will print this again and again and again\n");
 printf("For eternity until the heat-death of the universe.\n");
```

```
printf("Or until you hit CTRL-C.\n");
```

# 3.3.5 The Switch Statement

Depending on what languages you're coming from, you might or not be familiar with switch, or C's version might be even more restrictive than you're used to. This is a statement that allows you to take a variety of actions depending on the value of an integer expression.

Basically, it evaluates an expression to an integer value, jumps to the case that corresponds to that value. Execution resumes from that. If a break statement is encountered, then execution jumps out of the switch.

Let's do an example where the user enters a number of goats and we print out a gut-feel of how many goats that is.

```
#include <stdio.h>
```

```
int main(void) {
 int goat_count;
```

```
printf("Enter a goat count: ");
 scanf("%d", &goat_count); // Read an integer from the keyboard
```