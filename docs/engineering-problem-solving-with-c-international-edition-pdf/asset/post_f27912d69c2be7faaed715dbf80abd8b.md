
Notice that this function prototype requires two formal parameters. Because friend functions are not member functions, there is no calling object. Instead, we must include both operands as formal parameters in the function prototype and the function header. The following code segment illustrates the use of this function:

```
Pixel p1, p2(100, 200, 100), p3(10, 20, 30);
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
/* ........................................................ */
/* Addition (+) operator as friend function. */
/* File name: Pixel.cpp */
/* ........................................................ */
Pixel operator+(Pixel p1, Pixel p2)
{
    Pixel temp;
    temp.red = p1.red + p2.red;
    temp.green = p1.green + p2.green;
    temp.blue = p1.blue + p2.blue;
    return temp;
}
/* ........................................................ */
```

![](img/f2bfa570e453b020c16e048c79a3ea0e_518_0.png)

Notice that the keyword friend is not included in the function definition. friend status can only be granted in the class declaration. Compare this function definition with the member function definition. Since this function is not a member function, there is no calling object, and the references to red, green, and blue in the member function definition have been replaced by references to p1.red, p1.green, and p1.blue in the definition of the friend function.

## Practice!

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

The << operator cannot be defined as a member function of the pixel class because the first argument of the function must be an ostream reference. However, the function needs to access the private data members of the Pixel argument, so we declare it to be a friend function of the Pixel class. For efficiency, we have chosen to make the second formal parameter a const pass by reference instead of a pass by value. This allows a reference to be passed, but prevents modification of the argument pointed to by the reference. The function definition is as follows:

```
/*
 * Output << operator.
 *
 * File name: Pixel.cpp
 *
 */
ostream& operator<<(ostream& out, const Pixel& p)
{
    out << p.red << ',';
    out << p.green << ',';
    out << p.blue;
    return out;
}
/* ---------------------------------------------------------- */
```

The function must return an ostream reference, thus the statement return out; is required.

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

We can also use our << function to send output to a file. Recall that the ofstream class is derived from the ostream class. Thus, all ostream operations can also be applied to ofstream objects. The following code segment uses our << function to write to the file pixel.dat.

```
...
Pixel p1, p2(255);
ofstream outfile("pixel.dat");
outfile << "P1: " << p1 << " P2: " << p2 << endl;
...
```

![](img/f2bfa570e453b020c16e048c79a3ea0e_519_0.png)

![](img/f2bfa570e453b020c16e048c79a3ea0e_519_1.png)

The output written to the file pixel.dat is

```
P1: 0 0 0 P2: 255 255 255
```

Notice that our << function does not output a newline following the value of the Pixel. This allows us to output multiple Pixel values on the same line and is consistent with the performance of output operators defined for the built-in data types.

## The >> Operator

Our Pixel class declaration includes a function to overload the >> operator. The function has the following prototype:

```
friend istream& operator>>(istream& in, Pixel& p);
```

This function is defined as a friend function with two formal parameters, and the function returns an istream reference. The >> operator cannot be defined as a member function of the Pixel class because the first argument must be an istream reference. However, the function needs access to the private data members of the pixel argument, so we have declared the function to be a friend function of the Pixel class.

Since the function is defined to input a Pixel value, the function must modify the object referenced by the formal parameter, p. Therefore, this formal parameter must be a pass by reference. The function definition follows:

```
/*
 * Input (>>) operator.
 * File name: Pixel.cpp
 */
istream& operator>>(istream& in, Pixel& p)
{
    in >> p.red >> p.green >> p.blue;
    return in;
}
/*----------------------------------------------------------*/
```

This function must return an istream reference.

Overloading the >> operator is similar to overloading the << operator, except that the potential for encountering errors on input is greater. The function attempts to input three integer values to be assigned to the red, green, and blue data members of p. This function looks to the input stream for three integer values, separated by whitespace. Any unexpected character in the input stream, such as a comma or a colon, will place the istream in a fail state.

If our Pixel class required a special format for input, our >> function would need to check for the required format. If the required format was not encountered, the function would need to place the istream in a fail state. For illustration, assume that the format for entering a Pixel value required the integer values to be separated by a colon, as in

```
100:150:100
```

Our function can be modified to check for this format and place the istream in a fail state if the format is not correct:

```
/*
 * Input (>>) operator.
 *
 * Expected Pixel format is 100;150;100
 *
 * File name: Pixel.cpp
 *
 */
istream& operator>>(istream& in, Pixel& p)
{
    // Declare local objects.
    char ch;

    // Input integer value for red data member.
    in >> p.red;

    // Input colon. If colon not encountered.
    // set error state and return.
    in >> ch;
    if(ch != ':')
    {
        in.setstate(ios::failbit);
        return in;
    }

    // Input integer value for green data member.
    in >> p.green;

    // Input colon. If colon not encountered.
    // set error state and return.
    in >> ch;
    if(ch != ':')
    {
        in.setstate(ios::failbit);
        return in;
    }

    // Input integer value for blue data member.
    in >> p.blue;

    return in;
}
/*--------------------------------------------------------------*/
```

In this function definition, the function `setstate()` is used to place the `istream` in a fail state. The function `setstate()` is a member function of the `istream` class. In the statement

```
in.setstate(ios::failbit);
```

the `istream` object referenced by `in` calls the `setstate` function, and the `failbit` is set to true.

Another potential error when using the Pixel class is assigning a value greater than 255 to one or more of the data members. Handling potential overflow errors is discussed in the following section.

## Validating Objects

Recall that we defined a pixel as red, green, and blue triple, where each value in the triple ranges from 0 to 255. The Pixel class includes three data members (red, green, and blue) of type unsigned int. The data type unsigned int prevents the occurrence of a negative value, but it does not prevent a value from exceeding the maximum of 255. Consider the following example that uses the Pixel class:

```
/* Program chapter10_2 ---------------------------------------*/
/* Driver program for testing Pixel class */
#include "Pixel.h" //Required for Pixel
#include <iostream> //Required for cout
using namespace std;
int main()
{
    //Test constructors
    Pixel defaultP;
    Pixel grayP(100);
    Pixel redP(255, 0, 0);
    //Test output operator
    cout << "Default pixel: " << defaultP << endl;
    cout << "Gray pixel: " << grayP << endl;
    cout << "Red pixel: " << redP << endl;
    //Test arithmetic operators
    defaultP = grayP + redP;
    cout << "After addition, defaultP: " << defaultP << endl;
    return 0;
}
```

A sample run of this program is provided below:

```
Ingbers-MacBook-Pro:Programs jaingber$ g++ main.cpp Pixel.cpp
Ingbers-MacBook-Pro:Programs jaingber$ ./a.out
Default pixel: 0 0 0
Gray pixel: 100 100 100
Red pixel: 255 0 0
After addition. defaultP: 355 100 100
```

We see that the red value of defaultP has exceeded the maximum of 255. If any of the data members of a Pixel object exceeds the maximum value, unexpected results can occur when using the Pixel class to modify an image. To handle this situation, we will follow the model of the istream class, discussed in the previous section. The Pixel
