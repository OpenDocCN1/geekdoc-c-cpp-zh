
```
//Output operator.
friend ostream& operator <<(ostream& out, const Pixel& p);

private:
    unsigned int red, green, blue;
};
/**
```

The class declaration includes prototypes for a set of constructors; the arithmetic operators +, -, *, and /; and the operators << and >>. The keyword friend is used in the prototypes for the input and output operators. A friend function is not a member function; however, the keyword friend provides the function with access to the private and protected data members of the friendly class. This violates the guidelines for encapsulation but allows for programmer-defined types to be used in the same way as built-in types. Overloading of operators and friend functions are discussed in the sections that follow.

## Arithmetic Operators

Our Pixel class declaration includes the following prototypes:

```
Pixel operator+(const Pixel& p) const;
Pixel operator+(double v) const;
Pixel operator/(unsigned v) const;
```

Each prototype specifies a return type of Pixel, indicating that each method will return a value of type Pixel and that each method has one formal parameter. The keyword const following the parameter list prevents modification of the calling object.

### The + Operator

The method Pixel operator+(Pixel p) const has one formal parameter of type Pixel. Because this method is a member of the Pixel class, it will be called by a Pixel object. The calling object will provide the first operand for the + operator, and the argument will provide the second operand. The implementation of the overloaded addition operator is provided below.

```
/**
-----------------------------------------------------------*/
/* Addition (+) operator.                                  */
/* File name: Pixel.cpp                                    */
/*-----------------------------------------------------------*/
Pixel Pixel::operator+(const Pixel& p) const
{
    Pixel temp;
    temp.red = red + p.red;
    temp.green = green + p.green;
    temp.blue = blue + p.blue;
    return temp;
}
/*-----------------------------------------------------------*/
```

We can call the + operator as illustrated here:

```
Pixel p1, p2(100,200,100), p3(10,20,30);
p1 = p2 + p3; //function call
cout << p1;
...
```

In statement

```
p1 = p2 + p3;
```

p2 is the calling object and p3 is the argument. When the + operator is called, the formal parameter p receives the value of the argument, p3. The method references the private data members (red, green, and blue) of the calling object and the private members (p.red, p.green, and p.blue) of the formal parameter. The function also references the private data members of the local object temp (temp.red, temp.green, and temp.blue). The three assignment statements in the function definition

```
temp.red = red + p.red;
temp.green = green + p.green;
temp.blue = blue + p.blue;
```

assign to the local object temp the result of adding the function argument to the calling object. The value of temp is returned and assigned to the Pixel p1. The output generated when p1 is printed to the screen is

110 220 130

A program trace of these statements is provided in Figure 10.1.

### The * Operator

The function Pixel operator*(double v) const has one formal parameter of type double. The calling object will provide the first operand for the * operator, and the function argument will provide the second operand. The following is the function definition:

```
/* -------------------------------------------------------------- */
/* Multiplication (*) operator. */
/* File name: Pixel.cpp */
/* Pixel Pixel::operator*(double v) const
{
    Pixel temp;
    temp.red = red*v;
    temp.green = green*v;
    temp.blue = blue*v;
    return temp;
}
/* -------------------------------------------------------------- */
```

| main() | Memory Snapshot | | |
|---|---|---|---|
| Step 1: p1 = p2 + p3; | Pixel p1: 0 unsigned int red, 0 int green, 0 unsigned int blue | Pixel p2: 100 unsigned int red, 200 int green, 100 unsigned int blue | Pixel p3: 10 unsigned int red, 20 int green, 30 unsigned int blue |
| operator+(Pixel p) | | | |
| Step 2: Pixel temp; | Pixel temp: 10 unsigned int red, 20 int green, 30 unsigned int blue | Pixel temp: 0 unsigned int red, 0 int green, 0 unsigned int blue | |
| Step 3: temp.red = red + p.red; | Pixel temp: 110 unsigned int red, 0 int green, 0 unsigned int blue | | |
| Step 4: temp.green = green + p.green; | Pixel temp: 110 unsigned int red, 220 int green, 0 unsigned int blue | | |
| Step 5: temp.blue = blue + p.blue; | Pixel temp: 110 unsigned int red, 220 int green, 130 unsigned int blue | | |
| Step 6: return temp; | Pixel p1: 110 unsigned int red, 220 int green, 130 unsigned int blue | Pixel p2: 100 unsigned int red, 200 int green, 100 unsigned int blue | Pixel p3: 10 unsigned int red, 20 int green, 30 unsigned int blue |

## Figure 10.1 Program trace.

We can call the operator* function as follows:

```
Pixel p1, p2(100, 200, 100);
double factor{1.2};
p1 = p2*factor;
cout << p1;
...
```

| main() | Memory Snapshot | |
|---|---|---|
| Step 1: Pixel p1, p2(100, 200, 100); | Pixel p1 0 unsigned int red 0 unsigned int green 0 unsigned int blue | Pixel p2 100 unsigned int red 200 unsigned int green 100 unsigned int blue |
| Step 2: double factor(1.2); | double factor 1.2 | |
| Step 3: p1 = p2*factor; | | |
| operator*(double v) | | |
| Step 4: Pixel temp; | Pixel temp 0 unsigned int red 0 unsigned int green 0 unsigned int blue | double v 1.2 |
| Step 5: temp.red = red*v; Step 6: temp.green = green*v; Step 7: temp.blue = blue*v; | Pixel temp 120 unsigned int red 240 unsigned int green 120 unsigned int blue | |
| Step 8: return temp; | | |
| | Pixel p1 120 unsigned int red 240 unsigned int green 120 unsigned int blue | Pixel p2 100 unsigned int red 200 unsigned int green 100 unsigned int blue |

## Figure 10.2 Program trace.

In this example, p2 is the calling object and factor is the function argument. When the function operator* is called, the formal parameter v receives the value of factor. The local object temp is assigned the result of multiplying each data member of the calling object by the floating-point value v. The value of temp is returned and assigned to the Pixel p1. The output generated when p1 is printed to the screen is

```
120 240 120
```

A program trace is provided in Figure 10.2 to illustrate the passing of information. Note that this function does not define multiplication of two pixels, but rather defines multiplication of a Pixel by a double. If we want to define multiplication of two pixels,

![](img/0235a4ea835dc4575bd036e024a533b3_563_0.png)

we can include a function with the following prototype in our Pixel class definition:

```
Pixel operator*(Pixel p) const;
```

### The / Operator

The function Pixel operator/(int v) const has one formal parameter of type int. The calling object will provide the first operand for the / operator, and the function argument will provide the second operand. The function definition is the following:

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

![](img/0235a4ea835dc4575bd036e024a533b3_564_0.png)

The overloaded operator functions defined above are member functions of the pixel class. Thus, each function must be called by a Pixel object. This creates a limitation in the use of these operators; the first operand must be a Pixel object. Consider the following code segment that uses the + operator:
