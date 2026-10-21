First four operators are self-explanatory. The reminder operator can be used only with integers. For all other operators if one of the operands is float and second one is int then result will be in float.

The percentage symbol "%" is used for modulus of a number. a/b produces quotient and a%b where % is called remainder operator produces remainder when a is divided by b. The mathematical formula behind remainder operator is :
a % b = a – (a / b) * b (where a / b is integer division)
% operator works only with integer operands. Never use float operands. C++ does not allow float operand with % operator.

```
/*PROG 3.1 DEMO OF ARITHMETIC OPERATORS */
#include <iostream.h>
void main()
{
int a,b,sum,sub,div,mul,rem;
cout << "Enter two numbers\n";
cin >> a >> b;
sum = a+b;
sub = a-b;
div = a/b;
mul = a*b;
rem = a%b;
cout << "Sum of " << a << " and " << b << " is " << sum << endl;
cout << "Sub of " << a << " and " << b << " is " << sub << endl;
cout << "Div of " << a << " and " << b << " is " << div << endl;
cout << "Mul of " << a << " and " << b << " is " << mul << endl;
cout << "Rem of " << a << " and " << b << " is " << rem << endl;
}

OUTPUT :
Enter two numbers
35 20
Sum of 35 and 20 is 55
Sub of 35 and 20 is 15
Div of 35 and 20 is 1
Mul of 35 and 20 is 700
Rem of 35 and 20 is 15
```