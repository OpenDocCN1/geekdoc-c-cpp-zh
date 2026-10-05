```
cout << "Enter sign (+, -, *, /);";
cin >> sign;
if(sign == '+') || sign == '-' || sign == '*' || sign == '/')
{
    if(sign == '/' && z2.im == 0)
    {
        cout << "Division by zero is not allowed\n";
    }
    else
    {
        z = operation(z1, z2, sign);
        cout << "z = " << z1 << " sign << "z2 = " << z.re << " << " << z.im << " <<\n";
    }
}
else
{
    cout << "Wrong sign\n";
    return 0;
}
```

Complex operation (Complex a1, Complex a2, char sign)
{
double div;
Complex a;
switch(sign)
{

```
case '+':
    a.re = a1.re + a2.re;
    a.im = a1.im + a2.im;
break;
case '-':
    a.re = a1.re - a2.re;
    a.im = a1.im - a2.im;
break;
case '*':
    a.re = (a1.re*a2.re) - (a1.im*a2.im);
    a.im = (a1.im*a2.re) + (a1.re*a2.im);
break;
case '/':
    div = (a2.re*a2.re) + (a2.im*a2.im);
    a.re = ((a1.re*a2.re) + (a1.im*a2.im))/div;
    a.im = ((a1.im*a2.re) - (a1.re*a2.im))/div;
break;
return a;
```

**Comments:** That we're using the showpos manipulator, as discussed in Chapter 3, in order to prefix the positive values with +. The reason I did not pass the addresses of the structures to operation() in order to avoid the creation of copies, is to show you an example of a function with parameters structures.

**C.138** Define the structure type with members: name, code, and grade. Write a program that uses this type to read the data of 100 students and store them in an array of structures. If the user enters -1 for grade, the insertion of data should terminate. Write a function to sort the structures in grade