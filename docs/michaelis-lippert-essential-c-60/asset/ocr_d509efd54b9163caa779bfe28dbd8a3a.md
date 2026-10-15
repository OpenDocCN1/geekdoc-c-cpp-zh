# TABLE 12.1: Lambda Expression Notes and Examples

| Statement | Example |
|---|---|
| Lambda expressions themselves do not have a type. Therefore, there are no members that can be accessed directly from a lambda expression, not even the methods of object. | // ERROR: Operator '.' cannot be applied to
// operand of type 'lambda expression'
string s = ((int x) => x).ToString(); |
| Lambda expressions do not have a type and so cannot appear to the left of an is operator. | // ERROR: The first operand of an 'is' or 'as'
// operator may not be a lambda expression or
// anonymous method
bool b = ((int x) => x) is Func<int, int>; |
| A lambda expression can be converted only to a compatible delegate type; here an int-returning lambda may not be converted to a delegate type that represents a bool-returning method. | // ERROR: Lambda expression is not compatible
// with Func<int, bool> type.
Func<int, bool> f = (int x) => x; |
| A lambda expression does not have a type, so it cannot be used to infer the type of a local variable. | // ERROR: Cannot assign Lambda expression to
// an implicitly typed local variable
var v = x => x; |
| Jump statements (break, goto, continue) inside lambda expressions cannot be used to jump to locations outside the lambda expression, and vice versa. Here the break statement inside the lambda would jump to the end of the switch statement outside the lambda. | // ERROR: Control cannot leave the body of an
// anonymous method or Lambda expression
string[] args;
Func<string> f;
switch(args[0])
{
  case "/File":
    f = () =>
    {
      if (!File.Exists(args[1]))
        break;
      return args[1];
    };
  // ...
} |
| Parameters and locals introduced by a lambda expression are in scope only within the lambda body. | // ERROR: The name 'first' does not
// exist in the current context
Func<int, int, bool> expression =
  (first, second) => first > second;
first++; |