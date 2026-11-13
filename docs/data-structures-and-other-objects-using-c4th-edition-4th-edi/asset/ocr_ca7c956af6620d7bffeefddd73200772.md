# (FIGURE 7.5 continued)

```
void evaluate_stack_tops(stack<double>& numbers, stack<char>& operations)
// Library facilities used: stack
{
    double operand1, operand2;
    operand2 = numbers.top();
    numbers.pop();
    operand1 = numbers.top();
    numbers.pop();
    switch (operations.top())
    {
        case '+': numbers.push(operand1 + operand2);
                  break;
        case '-': numbers.push(operand1 - operand2);
                  break;
        case '*': numbers.push(operand1 * operand2);
                  break;
        case '/': numbers.push(operand1 / operand2);
                  break;
    }
    operations.pop();
}
```

# A Sample Dialogue

Type a fully parenthesized arithmetic expression:
( ( 60 + 40/50 ) * ( 16 - 4 ) )
That evaluates to 24

# Evaluating Arithmetic Expressions—Implementation

The implementation of read_and_evaluate in Figure 7.5 benefits from three of the istream functions:

+   • The name of the istream, ins, is used as part of the boolean expression that controls the loop. As we have seen before, the expression ins remains true so long as ins has not encountered bad input (such as the end of the file).
+   • The function call ins.peek() returns the next character of the ins input stream (without actually reading it).
+   • The function call ins.ignore() reads and discards the next character from the ins input stream.

Our implementation also uses three other functions, which we discuss next.