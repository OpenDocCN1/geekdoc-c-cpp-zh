When you define a function that takes an argument, you declare a variable, or formal argument, in the function definition. Then the value passed in a function call is assigned to this variable, which can now be used in the function.

# Review Questions

You’ll find answers to the review questions in Appendix A, “Answers to the Review Questions.”

+   1. Assume all variables are of type int. Find the value of each of the following variables:
+      a. x = (2 + 3) * 6;
+      b. x = (12 + 6)/2*3;
+      c. y = x = (2 + 3)/4;
+      d. y = 3 + 2*(x = 7/2);
+   2. Assume all variables are of type int. Find the value of each of the following variables:
+      a. x = (int) 3.8 + 3.3;
+      b. x = (2 + 3) * 10.5;
+      c. x = 3 / 5 * 22.0;
+      d. x = 22.0 * 3 / 5;
+   3. Evaluate each of the following expressions:
+      a. 30.0 / 4.0 * 5.0;
+      b. 30.0 / (4.0 * 5.0);
+      c. 30 / 4 * 5;
+      d. 30 * 5 / 4;
+      e. 30 / 4.0 * 5;
+      f. 30 / 4 * 5.0;
+   4. You suspect that there are some errors in the next program. Can you find them?

```
int main(void)
{
    int i = 1,
    float n;
    printf("Watch out! Here come a bunch of fractions!\n");
    while (i < 30)
        n = 1/i;
        printf("%f", n);
```