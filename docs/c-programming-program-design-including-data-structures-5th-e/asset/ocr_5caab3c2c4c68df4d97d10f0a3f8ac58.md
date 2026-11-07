Note that the function `exit` terminates the program.

# Function `evaluateOpr`

This function (if possible) evaluates an expression. Two operands are needed to evaluate an operation, and operands are saved in the stack. Therefore, the stack must contain at least two numbers. If the stack contains fewer than two numbers, then the expression has an error. In this case, the entire expression is discarded, and an appropriate message is printed. This function also checks for any illegal operations. In pseudocode, this function is:

```
if stack is empty
{
    error in the expression
    set expressionOk to false
}
else
{
    retrieve the top element of stack into op2
    pop stack
    if stack is empty
    {
        error in the expression
        set expressionOk to false
    }
    else
    {
        retrieve the top element of stack into op1
        pop stack

        //If the operation is legal, perform the
        //operation and push the result onto the stack.
        switch (ch)
        {
            case '+':
                //Perform the operation and push the result
                //onto the stack.
                stack.push(op1 + op2);
                break;
            case '-':
                //Perform the operation and push the result
                //onto the stack.
                stack.push(op1 - op2);
                break;
            case '*':
                //Perform the operation and push the
                //result onto the stack.
                stack.push(op1 * op2);
                break;
            case '/':
                //If (op2 != 0), perform the operation and
                //push the result onto the stack.
                stack.push(op1 / op2);
```