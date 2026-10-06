100 values of the grades array (assuming that sum was set to 0 before the loop entered.

As with other types of variables, you must declare arrays before you can use them. Declaring an array involves declaring the type of element that will be contained in the array, such as int, float, or an object, as well as the maximum number of elements that will be stored inside the array.

The definition

```
Fraction *fracts [100];
```

defines fracts to be an array containing 100 fractions. You can make valid references to this array by using subscripts 0–99.

The expression

```
fracts[2] = [fracts[0] add: fracts[1]];
```

invokes the Fraction's add: method to add the first two fractions from the fracts array and stores the result in the third location of the array.

Program 13.1 generates a table of the first 15 Fibonacci numbers. Try to predict its output. What relationship exists between each number in the table?

# Program 13.1

```
// Program to generate the first 15 Fibonacci numbers
#import <Foundation/Foundation.h>

int main (int argc, char * argv[])
{
    @autorelease {
```