
Pixel p1, p2(100, 200, 100), p3(10, 20, 30);
p1 = p2 + p3; // Valid.
p1 = p2 + 100; // Valid.
p1 = 100 + p2; // Invalid!

The first assignment statement

```
p1 = p2 + p3; // Valid.
```

is valid, since both operands of the + operator are Pixel objects. The second assignment statement

```
p1 = p2 + 100; // Valid.
```

is also valid, since the first operand, the calling object, is a Pixel object. The second operand is an integer, not a Pixel. However, since our Pixel class includes a constructor with one integer argument, this constructor is used to promote the integer 100 to a Pixel object with the value (100,100,100) and the function call is successful. The third statement

```
p1 = 100 + p2; // Invalid!
```

is not valid, since the first operand, the calling object, is an integer object, rather than a Pixel object. This statement will generate an error at compile time. This limitation can be removed by defining operators as friend functions instead of member functions.

## Practice 10.1

- Assume the following prototypes have been added to the Pixel class declaration.
- Write function definitions for each of the following methods.

- 1. Pixel operator/(Pixel p1); // divide a pixel by a pixel
- 2. bool operator==(Pixel p1); // return true if p1 is
  // equivalent to calling object

## friend Functions

A friend function is not a member function; however, a friend function does have access to the private data members of the class in which it is included. To declare a function as a friend function, the function prototype in the class declaration must begin with the keyword friend. Since a friend function is not a member function, the function is not affected by the public or private keywords. In our Pixel class, we include the friend functions in the public section, along with the other operator functions.

If we wanted to define the + operator as a friend function rather than as a member function, the prototype would be:

```
friend Pixel operator+(Pixel p1, Pixel p2);
```

Notice that this function prototype requires two formal parameters. Because friend functions are not member functions, there is no calling object. Instead, we must include both operands as formal parameters in the function prototype and the function header. The following code segment illustrates the use of this function:

```
Pixel p1, p2(100,200,100), p3(10,20,30);
p1 = p2 + p3; // Valid.
p1 = p2 + 100; // Valid.
p1 = 100 + p2; // Valid!
```

The third assignment statement

```
p1 = 100 + p2; // Valid!
```

is now a valid statement. The integer 100 provides the first argument of the + function, and p2 provides the second argument. Since the function is expecting Pixel objects as arguments, a constructor is used to promote the integer 100 to the Pixel object (100,100,100), and the function call is successful. The definition of the function is as follows:

```
/*---------------------------------------------*/
/* Addition (+) operator as friend function.   */
/* File name: Pixel.cpp                        */
/************************************************/
Pixel operator+(Pixel p1, Pixel p2)
{
    Pixel temp;
    temp.red = p1.red + p2.red;
    temp.green = p1.green + p2.green;
    temp.blue = p1.blue + p2.blue;
    return temp;
}
/*---------------------------------------------*/
```

![](img/0235a4ea835dc4575bd036e024a533b3_566_0.png)

Notice that the keyword friend is not included in the function definition. friend status can only be granted in the class declaration. Compare this function definition with the member function definition. Since this function is not a member function, there is no calling object, and the references to red, green, and blue in the member function definition have been replaced by references to p1.red, p1.green, and p1.blue in the definition of the friend function.

## Practice 10.2

Assume that the following function prototypes have been added to the Pixel class declaration. Write function definitions for each of the functions.

- 1. friend Pixel operator*(Pixel p1, Pixel p2);
- 2. friend Pixel operator/(Pixel p1, Pixel p2);
- 3. friend Pixel operator-(Pixel p1, Pixel p2);

## The << Operator

Our Pixel class declaration includes a function to overload the << operator. The function has the following prototype:

```
friend ostream& operator<<(ostream& out, const Pixel& p);
```

This function is defined as a friend function with two formal parameters, and the function returns an ostream reference. Returning an ostream reference supports chaining. Thus, we can output multiple expressions in a single output statement, as illustrated in the following statement:

```
cout << p1 << ', ' << p2 << endl;
```

The << operator cannot be defined as a member function of the Pixel class because the first argument of the function must be an ostream reference. However, the function needs to access the private data members of the Pixel argument, so we declare it to be a friend function of the Pixel class. For efficiency, we have chosen to make the second formal parameter a const pass by reference instead of a pass by value. This allows a reference to be passed, but prevents modification of the argument pointed to by the reference. The function definition is as follows:

```
/*------------------------------------------------------------*/
/* Output << operator.                                        */
/* File name: Pixel.cpp                                       */
/*------------------------------------------------------------*/
ostream& operator<<(ostream& out, const Pixel& p)
{
   out << p.red << ' ';
   out << p.green << ' ';
   out << p.blue;
   return out;
}
/*------------------------------------------------------------*/
```

![](img/0235a4ea835dc4575bd036e024a533b3_567_0.png)

> The function must return an ostream reference, thus the statement
> return out;
> is required.

Our function outputs the red, green, and blue values of the Pixel p, separated by whitespace. We can use the function as follows:

```
Pixel p1, p2(100, 200, 100);
cout << "P1: " << p1 << " P2: " << p2 << endl;
...
```

The output printed to the screen is

```
P1: 0 0 0 P2: 100 200 100
```

We can also use our << function to send output to a file. Recall that the ofstream class is derived from the ostream class. Thus, all ostream operations can also be applied to ofstream objects. The following code segment uses our << function to write to the file Pixel.dat.

```
...
Pixel p1, p2(255);
ofstream outfile("Pixel.dat");
outfile << "P1: " << p1 << " P2: " << p2 << endl;
...
```

The output written to the file Pixel.dat is

```
P1: 0 0 0 P2: 255 255 255
```

> Notice that our << function does not output a newline following the value of the Pixel. This allows us to output multiple Pixel values on the same line and is consistent with the performance of output operators defined for the built-in data types.

## The >> Operator

Our Pixel class declaration includes a function to overload the >> operator. The function has the following prototype:

```
friend istream& operator>>(istream& in, Pixel& p);
```

This function is defined as a friend function with two formal parameters, and the function returns an istream reference. The >> operator cannot be defined as a member function of the Pixel class because the first argument must be an istream reference. However, the function needs access to the private data members of the Pixel argument, so we have declared the function to be a friend function of the Pixel class.

Since the function is defined to input a Pixel value, the function must modify the object referenced by the formal parameter, p. Therefore, this formal parameter must be a pass by reference. The function definition follows:

```
/*-----------------------------------------------------------*
| Input (>>) operator.                                      |
| File name: Pixel.cpp                                      |
*-----------------------------------------------------------*/
istream& operator>>(istream& in, Pixel& p)
{
    in >> p.red >> p.green >> p.blue;
    return in;
}
/*-----------------------------------------------------------*/
```

> This function must return an istream reference.

Overloading the >> operator is similar to overloading the << operator, except that the potential for encountering errors on input is greater. The function attempts to input three integer values to be assigned to the red, green, and blue data members of p. This function looks at the input stream for three integer values, separated by whitespace. Any unexpected character in the input stream, such as a comma or a colon, will place the istream in a fail state.

If our Pixel class required a special format for input, our >> function would need to check for the required format. If the required format was not encountered, the function would need to place the istream in a fail state. For illustration, assume that the format for entering a Pixel value required the integer values to be separated by a colon, as in

```
100:150:100
```

Our function can be modified to check for this format and place the istream in a fail state if the format is not correct:
