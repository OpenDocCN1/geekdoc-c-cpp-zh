```
{
  Boolean result;
  int operand1, operand2;
  result = GetTwoOperands(operand1, operand2); //Pop 2 operands
  if (result == True) //If succeed, commit the calculation
    //and push the result to the stack

    switch (op) {
      case '+': S.Push(operand2+operand1);
        break;
      case '-': S.Push(operand2-operand1);
        break;
      case '*': S.Push(operand2*operand1);
        break;
      case '/': if (operand1 == 0) //Check whether the divisor is 0
        {
          cerr << "Divide by 0!" << endl;
          S.ClearStack();
          //Clear the stack if the divisor is 0
        } else
          S.Push(operand2/operand1);
          break;
      case '^': S.Push(pow(operand2,operand1));
        break;
    }
    cout<<=S.Peek() << ' '; //Output the result of calculation
  } else
    S.ClearStack();
}

Calculator::Calculator(void) //Constructor
{}

void Calculator::Run(void) //Read and process a postfix notation
{
  char c[20];
  while(cin >> c, *c != 'q') //Read an expression end with 'q'
```