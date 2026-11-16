# Performing Binary Operations on Mixed Data Types

If you perform binary operation on two different data types, the compiler will convert the data type that requires the fewer number of bits to the data type that requires the greatest number of bits for internal storage.

For example, if an int and a double are multiplied, the int is converted to a double before the multiplication because the double requires a larger number of bits for its internal representation than does an int. The result returned from the operation is converted to the data type that requires the largest number of bits for its representation, in this case a double.

See if you can figure out the output produced from the following program:

```
#include <stdio.h>

int main(void) {
   float f1 = 123.125, f2;
   int i1, i2 = 150;
   char c = 'a'; =99

   // float to int conversion
   i1 = f1;
   printf("%d\n", i1); 129

   // int to float conversion
   f1 = i2;
   printf("%f\n", f1); 150.000000

   // int divided by int
   f1 = i2 / 100;
   printf("%f\n", f1); 1.00

   // int divided by float
   f2 = i2 / 100.0;
   printf("%f\n", f2); 1.5
   return 0;
}
```

Here's the output:

```
123
150.000000
1.000000
1.500000
```