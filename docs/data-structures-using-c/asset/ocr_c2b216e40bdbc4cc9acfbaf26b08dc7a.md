# A.3 FUNCTIONS IN C++

There are two kinds of functions in C++, namely regular functions and member functions. Member functions those that are associated with a specific C++ class. Both types of functions are similar in all features excluding their scope.

A function consists of a function name, a list of arguments (input), a return type (output), and a body (code that implements a function). In Program Code A.4, Max is the function name, float a and float b are the list of arguments, where float is the return type, and the statements between { and } form the body of the function. Similarly, Square() is a function with int a as argument and int as the return type. Here, SayHello() is another function that has no argument, and it does not return any value, so its return type is void.

```
PROGRAM CODE A.4
// A sample C++ program-function
void SayHello()
{
cout << "Hello, welcome to the world of C with
classes";
}
int Square(int a)
{
return a * a;
}
float max(float a, float b)
{
if(a > b)
return a;
else
return b;
}
void main()
{
int x, y, z;
SayHello();
cout << endl;
cout << "Enter number";
cin >> x;
cout << "Square of " << x << " is " << Square(x);
cout << "\nEnter two integers";
cin >> y >> z;
cout << "Maximum between " << y << " and " << z <<
"is " << max(y, z);
}
```