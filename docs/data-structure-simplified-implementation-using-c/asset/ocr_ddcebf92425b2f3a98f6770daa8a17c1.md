```
// recursive function to multiply two numbers.
int multiply(int number, int times)
{
if(times==0)
return 0 ;
return number + multiply(number,times-1);
}
```

In the above function, a variable ‘times’ is used to multiply the number ‘number’ with the ‘times’. Variable ‘times’ value is decremented by one in each call. As soon as times reaches to 0, the value 0 is returned.

# C. Recursive function to compute the sum of two numbers

Two numbers can be added by using the recursive function. Consider the function named as sum that accepts two arguments ‘a’ and ‘b’ of integer type. To sum these two numbers ‘a’ and ‘b’, we add ‘1’ to a ‘b’ times. Eventually, total of these two numbers can be returned to the caller.

```
//function to return sum of a and b
int sum(int a, int b)
{
if(b==0)
return a;
return 1+sum(a,b-1);
}
```

In aforementioned function, number of calls will be governed by the value of ‘b’. For instance, if b=4, then function will be executed four times, once b is reached at 0, the value of first number i.e. a will be returned. Therefore, total will be a+1+1+1+1, eventually, ‘a+4’ will be returned to the caller.

# D. Recursive function to find a character in a string

Recursive function can also be used to determine, whether a given character exist in the string or not. For instance, if it is intended to compute whether character ‘c’ exist in the string “jitendra”, recursive function can be used. This function as described in the following example returns the integer value. If the character exist then it returns 1 else returns 0.

From the calling function three arguments are passed, first is string, second is the character and finally the integer ‘i’ that is equal to 0. Here ‘i’ is incremented in each call. Correspondingly, character passed as an argument is compared with each character of the given string one by one. As soon as character matches function terminates and returns