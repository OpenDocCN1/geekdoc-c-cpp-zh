
// recursive function to multiply two numbers.
int multiply(int number, int times)
{
if(times==0)
return 0 ;
return number + multiply(number,times-1);
}

In the above function, a variable ‘times’ is used to multiply the number ‘number’ with the ‘times’. Variable ‘times’ value is decremented by one in each call. As soon as times reaches to 0, the value 0 is returned.

## C. Recursive function to compute the sum of two numbers

Two numbers can be added by using the recursive function. Consider the function named as sum that accepts two arguments ‘a’ and ‘b’ of integer type. To sum these two numbers ‘a’ and ‘b’, we add ‘1’ to a ‘b’ times. Eventually, total of these two numbers can be returned to the caller.

//function to return sum of a and b
int sum(int a, int b)
{
if(b==0)
return a;
return 1+sum(a,b-1);
}

In aforementioned function, number of calls will be governed by the value of ‘b’. For instance, if b=4, then function will be executed four times, once b is reached at 0, the value of first number i.e. a will be returned. Therefore, total will be a+1+1+1+1, eventually, ‘a+4’ will be returned to the caller.

## D. Recursive function to find a character in a string

Recursive function can also be used to determine, whether a given character exist in the string or not. For instance, if it is intended to compute whether character ‘c’ exist in the string “jitendra”, recursive function can be used. This function as described in the following example returns the integer value. If the character exist then it returns 1 else returns 0.

From the calling function three arguments are passed, first is string, second is the character and finally the integer ‘i’ that is equal to 0. Here ‘i’ is incremented in each call. Correspondingly, character passed as an argument is compared with each character of the given string one by one. As soon as character matches function terminates and returns success. If there is no match, Null will be encountered, correspondingly unsuccessful is returned to the caller.

//function to find out the existence of a character in a string
int pattern(char str[20], char p, int i)
{
if(str[i]=='\0')   // No match
return 0;    //return unsuccessful
if(str[i]==p)      // matches
return 1;    //return successful
pattern(str,p,i+1);      //  call the same function, increment the value of ‘i’
}

## E. Recursive function to reverse a string

String can also be reversed with the help of recursion. In this case we can make use of the '\0' character inserted at the end of the string. This will facilitate in the termination of the string once the end of the string is reached. Complete program depicting the string reversal has been described below:

// to compute the reverse of the string
void reverse(char str[], int i=0)
{
if(str[i]!='\0')
reverse(str,i+1);
cout<<str[i];//Reversing the string character by character
}

In the above program, string is received in the reverse function. Here default function has been used. That initializes the value of ‘i’ to 0. In each call, value of i is incremented by 1. Once the string will reach to ‘\0’ then the recursion will terminate. It is followed by pop operation that will take place on recursive calls that has already occurred. Eventually, character by character will be displayed from the last value of ‘i’. Consequently, string will be reversed. Alternatively, we can also store it in temp variable and same can be utilized by the caller function.

## F. Function from decimal to binary

Converting from the decimal to binary using manual method is fairly simple. However, implementing it on computer is notably complex. This complexity has been eliminated with the help of recursive function. As in manual method, we compute the result till the number is not reaching to 0. Upon reaching to zero, the binary number is returned. If the number has not reached to zero in that case remainder is computed and the numbers are adjusted based on their significance (Based on position). From the main function, value of b and factor is passed as 0 and 1. Entire function has been depicted below.

//function to convert the decimal into binary
int dTobinary(int dec, int b, int factor)
{
if(dec<=0)
return b;
int rem=dec%2;
b=b+rem*factor;
return dTobinary(dec/2,b,factor*10);
}

## G. Function to reverse the digit

Recursion can also be used to compute the reverse of a given number, digit by digit. For instance, if the number is 704, then the answer will result into 407. Recursive function receives the value of a number and result from the main function. Value of number may be anything, whereas the value of variable ‘result’ is passed as 0. When number reaches to 0 it returns the result. Eventually, the result is returned to the caller. Entire function has been depicted below.

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

## H. Digit sum

To compute the sum of the digit, complete function has been depicted below. Corresponding to non-recursive function, majority of the logic remains same. Sum is computed by adding the variable the sum with the remainder. Consider that the value is passed is 365, so initially, sum would be 5, number will be reduced to 36 by the call sum_digit(num/10,sum), statement *sum=sum + remainder* will result in 5+6=11 since new remainder is 6. Finally, 3 will be send to a new call. It is not 0, consequently, rest of the statements would execute i.e. *11+3=14*,since new remainder will be 3. In the next call, num will become 0, therefore sum will be result to the caller. In this case it is 14.

//Digit sum of a number using recursion
int sum_digit(int num, int sum)
{
if(num==0)
{
return sum;
}
sum=sum+num%10;
return sum_digit(num/10,sum);
}  //end of function

In this function, from the main we have to pass two numbers, one for which we have to compute the sum. In the given case it is 365, the second number is sum that should be 0.

## I. Other recursive function

Many of the recursive function has already been discussed in this text book but are not included in order to mitigate redundancy. These recursive functions include

- Traversal of a BST.
- Creation of a tree.
- Height of a tree.
- Mirroring of a Tree.
- Binary search in a BST

Readers are requested to please refer these programs on the related chapters for the deeper understanding of the recursion.

## EXERCISE

## A. Descriptive Type Questions

- 1) What is recursion? Discuss the significance of recursion in modern programming language.
- 2) What is the significance of active record. What are the various components of active record.
- 3) What is the role of base condition? What will be the repercussion, if base condition is i) Not written ii) poorly written
- 4) How mutual function is different from the indirect function?
- 5) What are the usage of binary function? Discuss the base condition execution in the binary function.
- 6) Discuss the performance overhead involved in case of recursion.
- 7) What is stack and heap in recursive function. What is their significance in recursive function?
- 8) Explain the functioning of the tail recursion.
- 9) Write down the program to reverse the link list using recursion.
- 10) Write down the program to compute the GCD using recursion.
- 11) Compute the permutation of a number using recursion?
- 12) Compute the greater of two number using recursion (Don't use the if statement).
- 13) Write down the recursive function for the following equation.
  0 if n=0
  f(n)= f(2n) if n is odd
        1+f(n-1) if n is even
- 14) Write down the recursive function for the following equation.
  if n=0
  f(n)= n+ f(2n) if n is odd
        f(n-1)+f(n-2) if n is even

## B. Multiple Choice Answers

- 1. In recursion, function can call to another function. (True/False).
- 2. There may be recursive function that may not return the value to the caller (True/False).
- 3. Recursive function have better performance relative to the iterative function.
- 4. Recursive functions are always concise relative to iterative function (True/False).
