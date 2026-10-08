# 8.7.1 Unintentional Infinite Loops

These loops result from programming errors. They are not meant to run forever but do so due to mistakes in the code. Common causes include:

+   - Missing Increment/Decrement Statements:
If a loop variable is not updated within the loop body, the condition never changes, leading to an infinite loop.
- Incorrect Loop Conditions:
A single type, such as using = instead of ==, can make the loop condition always true, preventing the loop from exiting.
- Logic Errors in the Loop Body: Logic errors in the loop body can result in conditions that are always true, leading to infinite execution.

The following example demonstrates an unintentional infinite loop:

```
#include <stdio.h>

int main() {
    int i = 0;
    // Missing increment statement causes infinite loop
    while (i < 10) {
        printf("%d\n", i);
        // i++; // Uncomment this to fix the infinite loop
    }

    return 0;
}
```

> Tip: Always verify that your loop condition is correctly defined and that loop variables are modified inside the loop. To debug infinite loops, you can add print statements inside the loop to track variable changes. Once the issue is resolved, remove these debug statements. Alternatively, use a debugger for more efficient troubleshooting.

# 8.7.2 Intentional Infinite Loops

Intentional infinite loops are used in systems that require continuous operation

The code below simulates an LED blinking indefinitely using an infinite loop:

```
#include <stdio.h>
// Simulate an LED blinking in an embedded system
void blinkLED() {
    while (1) { // the loop condition is always true
```