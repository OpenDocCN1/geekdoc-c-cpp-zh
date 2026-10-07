# Arrays 249

sequences through the first 100 elements of the array grades (elements 0-99) adds the value of each grade into sum.When the loop is finished, the variable sum contains the total of the first 100 values of the grades array (assuming that sum was set to 0 before the loop was entered).

As with other types of variables, you must declare arrays before you can use them. Declaring an array involves declaring the type of element that will be contained in the array, such as int, float, or an object, as well as the maximum number of elements that will be stored inside the array.

The definition

```
fracts [100];
```

defines fracts to be an array containing 100 fractions.You can make valid references to this array by using subscripts 0-99.

The expression

```
fracts[2] = fracts[0] add: fracts[1];
```

invokes Fraction's method: to add the first two fractions from the fract array and stores the result in the third location of array.

Program 13.1 generates a table of the first 15 Fibonacci numbers.Try to predict its output. What relationship exists between each number in the table?

# Program 13.1

```
// Program to generate the first 15 Fibonacci numbers
#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {
    NSAutoreleasePool *pool = [NSAutoreleasePool alloc] init];
    Fibonacci[0] = 0; /* by definition *
    Fibonacci[1] = 1; /* dito */

    for (int i = 2; i < 15; ++i) {
        Fibonacci[i] = Fibonacci[i-2] + Fibonacci[i-1];
    }

    NSLog("@%d", Fibonacci[i]);
    [pool drain];
    return 0;
}
```

# Program 13.1 Output

```
0
1
1
2
3
5
```