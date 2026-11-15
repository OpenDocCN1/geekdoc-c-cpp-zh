we can include a function with the following prototype in our Pixel class definition:

```
Pixel operator*(Pixel p) const;
```

The / Operator The function Pixel operator/(int v) const has one formal parameter of type int. The calling object will provide the first operand for the / operator, and the function argument will provide the second operand. The function definition is the following:

```
/********************************************************************
/ * Division (/) operator.                                          *
/ *                                                                  *
/ * File name: Pixel.cpp                                             *
/ *                                                                  *
/********************************************************************/
Pixel Pixel::operator/(unsigned v) const
{
   Pixel temp;
   temp.red = red/v;
   temp.green = green/v;
   temp.blue = blue/v;
   return temp;
}
/********************************************************************/
```

We can call this function as illustrated below:

```
Pixel p1, p2(100, 200, 100);
p1 = p2/2;
cout << p1;
...
```

In this example, p2 is the calling object, and the integer 2 is the function argument. When the function is called, the formal parameter v receives the value of the argument. The local object temp is assigned the result of dividing the calling object by an integer value. The value of temp is returned and assigned to the Pixel p1. The output generated when p1 is printed to the screen is

```
50 100 50
```

Note that this function does not define division of two pixels, but rather defines division of a Pixel by an int. If we want to define division of two pixels, we can include a function with the following prototype in our Pixel class definition:

```
Pixel operator/(Pixel p) const;
```

![](bbox=[0.13, 0.88, 0.2, 0.94])

The overloaded operator functions defined above are member functions of the pixel class. Thus, each function must be called by a Pixel object. This creates a limitation in the use of these operators; the first operand must be a Pixel object. Consider the following code segment that uses the + operator: