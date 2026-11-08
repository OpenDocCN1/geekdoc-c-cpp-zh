In a while and for loop, the loop condition is evaluated before executing the body of the loop. Therefore, while and for loops are called **pretest loops**. On the other hand, the loop condition in a `do...while` loop is evaluated after executing the body of the loop. Therefore, `do...while` loops are called **posttest loops**.

Because the `while` and `for` loops both have entry conditions, these loops may never activate. The `do...while` loop, on the other hand, has an exit condition and therefore always executes the statement at least once.

# EXAMPLE 5-19

Consider the following two loops:

```
a.  i = 11;
    while (i <= 10)
    {
        cout << i << " ";
        i = i + 5;
    }
    cout << endl;

b.  i = 11;
    do
    {
        cout << i << " ";
        i = i + 5;
    }
    while (i <= 10);

    cout << endl;
```

In (a), the `while` loop produces nothing. In (b), the `do...while` loop outputs the number 11 and also changes the value of `i` to 16.

A `do...while` loop can be used for input validation. Suppose that a program prompts a user to enter a test score, which must be greater than or equal to 0 and less than or equal to 50. If the user enters a score less than 0 or greater than 50, the user should be prompted to re-enter the score. The following `do...while` loop can be used to accomplish this objective:

```
int score;

do
{
    cout << "Enter a score between 0 and 50: ";
    cin >> score;
    cout << endl;
}
while (score < 0 || score > 50);
```