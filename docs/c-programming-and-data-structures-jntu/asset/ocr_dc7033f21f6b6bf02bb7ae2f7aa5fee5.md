Another example of while statement which uses the keyboard input is shown below:

```
..........
.......... 
character = '';
while (character != 'Y')
    character = getchar();
xxxxxxxx;
..........
```

First the character is initialized to ''. The while statement then begins by testing whether character is not equal to Y. Since the character was initialized to '', the test is true and the loop statement

character = getchar();

is executed. Each time a letter is keyed in, the test is carried out and the loop statement is executed until the letter Y is pressed. When Y is pressed, the condition becomes false because character equals Y, and the loop terminates, thus transferring the control to the statement xxxxxxxx;

# Example 7.1

A program to evaluate the equation

$y = x^n$

when n is a non-negative integer, is given in Fig. 7.2.

The variable y is initialized to 1 and then multiplied by x, n times using the while loop. The loop control variable, count is initialized outside the loop and incremented inside the loop. When the value of count becomes greater than n, the control exits the loop.

# 7.3 THE DO STATEMENT

The while loop construct that we have discussed in the previous section makes a test of condition before the loop is executed. Therefore, the body of the loop may not be executed at all if the condition is not satisfied at the very first attempt. On some occasions it might be necessary to execute the body of the loop before the test is performed. Such situations can be handled with the help of the do statement. This takes the form:

```
do
{
    body of the loop
}
while (test-condition);
```

On reaching the do statement, the program proceeds to evaluate the body of the loop first. At the end of the loop, the test-condition in the while statement is evaluated. If the condition is true, the program continues to evaluate the body of the loop once again. This process continues as long as the condition is true. When the condition becomes false, the loop will be terminated and the control goes to the statement that appears immediately after the while statement.