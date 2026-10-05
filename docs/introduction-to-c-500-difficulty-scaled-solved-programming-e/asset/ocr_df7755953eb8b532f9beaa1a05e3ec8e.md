# 388 Introduction to C++

```
if(cl1->y > c2->y)
    height = cl1->y - c2->y;
else
    height = c2->y - cl1->y;

  return base*height; // Return the area.
```

C.13.7 For a complex number, we have z = a + bj, where j is the imaginary unit, a is the real part, and b is the imaginary part. Define the structure type Complex with members the float numbers re and im, and which represent the real and imaginary parts of a complex number. Write a function that takes as parameters two structures of type Complex and a character, which represents the sign of a math operation. The function should perform the math operation and return the result as a structure of type Complex. Write a program that uses the structure Complex to read two complex numbers and a math sign (+, -, /) and use the function to display the result of the math operation. If z1 = a + bj and z2 = c + dj we have:

```
z = z1 + z2 = (a+c)+(b+d)j

z = z1 - z2 = (a-c)+(b-d)j

z = z1 × z2 = (ac-bd)+(ad+bc)j

z = \frac{z1}{z2} = (\frac{ac+bd}{c^2+d^2} + \frac{ad-bc}{c^2+d^2})j
```

```
#include <iostream>
using std::cout;
using std::cin;
```

```
struct Complex
{
    double re; // The real part of the complex number.
    double im; // The imaginary part of the complex number.
};
```

```
Complex operation(Complex a1, Complex a2, char sign);
```

```
int main()
{
    char sign;
    Complex z1, z2, z;
```

```
cout << "Enter real and imaginary part of the first complex number: ";
cin >> z1.re >> z1.im;
cout << std::showpos << "z1 = " << z1.re << ' ' << z1.im << 'j' << '\n';
```

```
cout << "Enter real and imaginary part of the second complex number: ";
cin >> z2.re >> z2.im;
cout << "z2 = " << z2.re << ' ' << z2.im << 'j' << '\n';
```