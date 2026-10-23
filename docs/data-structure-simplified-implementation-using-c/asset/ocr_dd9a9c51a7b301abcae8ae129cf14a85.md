not reached to zero in that case remainder is computed and the numbers are adjusted based on their significance (Based on position). From the main function, value of b and factor is passed as 0 and 1. Entire function has been depicted below.

```
//function to convert the decimal into binary
int dTobinary(int dec, int b, int factor)
{
if(dec<=0)
return b;
int rem=dec%2;
b=b+rem*factor;
return dTobinary(dec/2,b,factor*10);
}
```

# G. Function to reverse the digit

Recursion can also be used to compute the reverse of a given number, digit by digit. For instance, if the number is 704, then the answer will result into 407. Recursive function receives the value of a number and result from the main function. Value of number may be anything, whereas the value of variable ‘result’ is passed as 0. When number reaches to 0 it returns the result. Eventually, the result is returned to the caller. Entire function has been depicted below.

```
//function to reverse the digit
int rev_digit(int number, int result)
{
if(number==0)
{
return result;
}
int rem=number%10;
result=result*10+rem;
return rev_digit(number/10,result);
}
```

# H. Digit sum

To compute the sum of the digit, complete function has been depicted below. Corresponding to non-recursive function, majority of the logic remains same. Sum is computed by adding the variable the sum with the remainder. Consider that the value is passed is 365, so initially, sum would be 5, number will be reduced to 36 by the call sum_digit(num/10,sum), statement