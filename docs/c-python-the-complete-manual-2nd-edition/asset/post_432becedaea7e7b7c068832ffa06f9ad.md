
## Data Types

```
cout.precision(22);
cout << PI;
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_108_0.png)

![](img/2f9c26fcf758b5bc56897d9c75b6347f_108_1.png)

Again, build and run the code; as you can see from the command line window, the number represented by the variable PI is different to the number you’ve told C++ to use in the variable. The output reads the value of PI as 3.141592653589793115998, with the numbers going awry from the fifteenth decimal place.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_108_2.png)

This is mainly due to the conversion from binary in the compiler and that the IEEE 754 double precision standard occupies 64-bits of data, of which 52-bits are dedicated to the significant (the significant digits in a floating-point number) and roughly 3.5-bits are taken holding the values 0 to 9. If you divide 53 by 3.5, then you arrive at 15.142857 recurring, which is 15-digits of precision.

To be honest, if you’re creating code that needs to be accurate to more than fifteen decimal places, then you wouldn’t be using C++, you would use some scientific specific language with C++ as the connective tissue between the two languages.

You can create your own data types, using an alias-like system called typedef. For example:

![](img/2f9c26fcf758b5bc56897d9c75b6347f_108_3.png)

```
#include <iostream>
using namespace std;
typedef int metres;
int main()
{
    metres distance;
    distance = 15;
    cout << "distance in metres is: " << distance;
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_108_4.png)

This code when executed creates a new int data type called metres. Then, in the main code block, there’s a new variable called distance, which is an integer; so you’re basically telling the compiler that there’s another name for int. We assigned the value 15 to distance and displayed the output: distance in metres is 15.

It might sound a little confusing to begin with but the more you use C++ and create your own code, the easier it becomes.

## Strings

Strings are objects that represent and hold sequences of characters. For example, you could have a universal greeting in your code ‘Welcome’ and assign that as a string to be called up wherever you like in the program.

There are different ways in which you create a string of characters, which historically are all carried over from the original C language, and are still supported by C++.

```
```cpp
#include <iostream>
using namespace std;

int main ()
{
}
```
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_109_0.png)

```
```cpp
char greet[8] = {'W', 'e', 'l', 'c', 'o', 'm', 'e', '\0'};
cout << greet << "\n";
```
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_109_0.png)

```
```cpp
char greet[] = "Welcome";
cout << greet << "\n";
```
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_109_2.png)

```
```cpp
string greet = "Welcome";
cout << greet << "\n";
```
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_109_2.png)

### STEP 5

There are also many different operations that you can apply with the string function. For instance, to get the length of a string you can use:

```
#include <iostream>
using namespace std;

int main ()
{
    string greet = "Welcome";
    cout << "The length of the string is: ";
    cout << greet.size() << "\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_110_0.png)

### STEP 6

You can see that we used greet.size() to output the length, the number of characters there are, of the contents of the string. Naturally, if you call your string something other than greet, then you need to change the command to reflect this. It’s always stringname.operation. Build and run the code to see the results.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_110_1.png)

### STEP 7

You can of course add strings together, or rather combine them to form longer strings:

```
#include <iostream>
using namespace std;

int main ()
{
    string greet1 = "Hello";
    string greet2 = ", world!";
    string greet3 = greet1 + greet2;

    cout << greet3 << "\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_110_2.png)

### STEP 8

Just as you might expect, you can mix in an integer and store something to do with the string. In this example, we created int length, which stores the result of string.size() and outputs it to the user:

```
#include <iostream>
using namespace std;

int main ()
{
    int length;
    string greet1 = "Hello";
    string greet2 = ", world!";
    string greet3 = greet1 + greet2;

    length = greet3.size();

    cout << "The length of the combined strings is: " << length << "\n";
}
```

### STEP 9

Using the available operations that come with the string function, you can manipulate the contents of a string. For example, to remove characters from a string you could use:

```
#include <iostream>
using namespace std;

int main ()
{
    string strg ("Here is a long sentence in a string.");
    cout << strg << '\n';

    strg.erase (10,5);
    cout << strg << '\n';

    strg.erase (strg.begin()+8);
    cout << strg << '\n';

    strg.erase (strg.begin()+9, strg.end()-9);
    cout << strg << '\n';
}
```

### STEP 10

It’s worth spending some time playing around with the numbers, which are the character positions in the string. Occasionally, it can be hit and miss whether you get it right, so practice makes perfect. Take a look at the screenshot to see the result of the code.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_110_3.png)

## C++ Maths

Programming is mathematical in nature and as you might expect, there’s plenty of built-in scope for some quite intense maths. C++ has a lot to offer someone who’s implementing mathematical models into their code. It can be extremely complex or relatively simple.

### C++ = MC²

The basic mathematical symbols apply in C++ as they do in most other programming languages. However, by using the C++ Math Library, you can also calculate square roots, powers, trig and more.

### STEP 1

C++’s mathematical operations follow the same patterns as those taught in school, in that multiplication and division take precedence over addition and subtraction. You can alter that though. For now, create a new file and enter:

```
#include <iostream>
using namespace std;

int main ()
{
    float numbers = 100;
    numbers = numbers + 10; // This adds 10 to the initial 100
    cout << numbers << "\n";
    numbers = numbers - 10; // This subtracts 10 from the new 110
    cout << numbers << "\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_111_0.png)

### STEP 2

While simple, it does get the old maths muscle warmed up. Note that we used a float for the numbers variable. While you can happily use an integer, if you suddenly started to use decimals, you would need to change to a float or a double, depending on the accuracy needed. Run the code and see the results.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_111_1.png)

### STEP 3

Multiplication and division can be applied as such:

```
#include <iostream>
using namespace std;

int main ()
{
    float numbers = 100;
    numbers = numbers * 10; // This multiplies 100 by 10
    cout << numbers << "\n";
    numbers = numbers / 10; // And this divides 1000 by 10
    cout << numbers << "\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_111_2.png)

### STEP 4

Again, execute the simple code and see the results. While not particularly interesting, it’s a start into C++ maths. We used a float here, so you can play around with the code and multiply by decimal places, as well as divide, add and subtract.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_111_3.png)

### STEP 5

The interesting maths content comes when you call upon the C++ Math Library. Within this header are dozens of mathematical functions along with further operations. Everything from computing cosine to arc tangent with two parameters, to the value of PI. You can call the header with:

```
#include <iostream>
#include <cmath>
using namespace std;

int main ()
{
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_112_0.png)

### STEP 6

Start by getting the square root of a number:

```
#include <iostream>
#include <cmath>
using namespace std;

int main ()
{
    float number = 134;

    cout << "The square root of " << number << " is: " << sqrt(number) << "\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_112_1.png)

### STEP 7

Here we created a new float called number and used the sqrt(number) function to display the square root of 134, the value of the variable, number. Build and run the code, and your answer reads 11.5758.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_112_2.png)

### STEP 8

Calculating powers of numbers can be done with:

```
#include <iostream>
#include <cmath>
using namespace std;

int main ()
{
    float number = 12;
    cout << number << " to the power of 2 is " << pow(number, 2) << "\n";
    cout << number << " to the power of 3 is " << pow(number, 3) << "\n";
    cout << number << " to the power of .08 is " << pow(number, 0.8) << "\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_112_3.png)

### STEP 9

Here we created a float called number with the value of 12, and the pow(variable, power) is where the calculation happens. Of course, you can calculate powers and square roots without using variables. For example, pow(12, 2) outputs the same value as the first cout line in the code.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_112_4.png)

### STEP 10

The value of Pi is also stored in the cmath header library. It can be called up with the M_PI function. Enter cout << M_PI; into the code and you get 3.14159; or you can use it to calculate:

```
#include <iostream>
#include <cmath>
using namespace std;

int main ()
{
    double area, radius = 1.5;
    area = M_PI * radius * radius;
    cout << area << "\n";
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_112_5.png)
