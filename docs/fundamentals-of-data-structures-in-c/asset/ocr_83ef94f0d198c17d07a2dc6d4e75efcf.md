# LOOPING STATEMENTS

1. Answer :
mmmm
aaaa
nnnn
EXPLANATION :
str[i], [i]str, *(str+i), *(i+str) are all different ways of expressing the same location in an array. Generally array name is the base address for that array. Here str is the base address for the array and i is the index number from the base address. So, indirecting it with * is same as str[i]. [i]str] may be surprising. But in the case of C it is same as str[i].

2. Answer :
2222223456
EXPLANATION :
Initially pointer arr is assigned to both ptr1 and ptr2. In the first loop, since only pt2 is incremented and not arr, the value 2 will be printed 5 times. In second loop ptr itself is incremented, hence you get the above output.

3. Answer :
J\MpvfIzPv
EXPLANATION :
++*str++ will be parse in the following order.
* *str is the value at each location currently pointed by str will be considered.
* ++*str the retrieved value will be incremented.
* When ; is encountered the location will be incremented that is str++ will be executed.
Hence you get the above output.

4. Answer :
Compiler error: Undefined label 'INDIA'
EXPLANATION :
The scope of the labels is limited to functions. The label 'INDIA' is available only in function func() Hence it is not visible in main() function.

5. Answer :
Compiler error: Lvalue required
EXPLANATION :
Array names are pointer constants. So it cannot be modified.

6. Answer :
1
EXPLANATION :
Before entering into the for loop the condition is evaluated, which evaluates to 0 (i.e., false) and exits from the loop. (Note the semicolon at the end of for loop), and a is incremented by 1, hence you get the above output.

7. Answer :
No Output.
EXPLANATION :
Inside the main() function i is an unsigned integer. It is compared with a signed value (i.e., -3). Since both data types doesn't match, the condition becomes false and control exits from loop, hence the printf() function will not be executed and you will not get any output from the program.