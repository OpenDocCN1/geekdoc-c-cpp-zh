```
~~~cpp
            //Otherwise, report the error.
            //Set expressionOk to false.
                break;
        otherwise operation is illegal
        {
            output an appropriate message;
            set expressionOk to false
        }
    } //end switch
}
~~~
```

Following this pseudocode, the definition of the function evaluateOpr is:

```
~~~cpp
void evaluateOpr( ofstream& out, stackType<double>& stack,
                  char& ch, bool& isExpOk)
{
    double op1, op2;

    if (stack.isEmptyStack())
    {
        out << " (Not enough operands)";
        isExpOk = false;
    }
    else
    {
        op2 = stack.top();
        stack.pop();

        if (stack.isEmptyStack())
        {
            out << " (Not enough operands)";
            isExpOk = false;
        }
        else
        {
            op1 = stack.top();
            stack.pop();

            switch (ch)
            {
            case '+':
                stack.push(op1 + op2);
                break;
            case '-':
                stack.push(op1 - op2);
                break;
            case '*':
                stack.push(op1 * op2);
                break;
            case '/':
                if (op2 != 0)
                    stack.push(op1 / op2);
~~~
```