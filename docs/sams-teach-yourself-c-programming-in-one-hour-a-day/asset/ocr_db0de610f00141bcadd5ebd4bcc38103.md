7. 2 bytes. Using bit fields, you could declare a structure as follows:
struct date
{
  unsigned month : 4;
  unsigned day : 5;
  unsigned year : 7;
}

This structure stores the data in 2 bytes (16 bits). The 4-bit month field can hold values from 0 to 15, sufficient for holding 12 months. Likewise, the 5-bit day field can hold values from 0 to 31, and the 7-bit year field can hold values from 0 to 127. You can assume that the year value will be added to 1900 to allow year values from 1900 to 2027.

8. 00000000

9. 00000101

10. These two evaluate to the same result. Using exclusive OR with 11111111 is the same using the complement operator: Each bit in the original value is reversed.

# Exercises

+   1. The code is as follows:
long *ptr;
ptr = malloc(1000 * sizeof(long));

+   2. The code is as follows:
long *ptr;
ptr = calloc(1000, sizeof(long));

+   3. Using a loop and assignment statement:
int count;
for (count = 0; count < 1000; count++)
data[count] = 0;

+   Using the memset() function:
memset(data, 0, 1000 * sizeof(float));

+   4. This code compiles and runs without error; however, the result is incorrect.
Because number1 and number2 are both integers, the result of their division is an integer, losing any fractional part of the answer. To get the correct answer, you need to cast the expression to type float:
answer = (float) number1/number2;