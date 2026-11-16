14. ANSWER : abc is a ptr to a function which takes 2 argument, an integer variable and a pointer to a funtion which returns void. The return type of the function abc() is of type void.
EXPLANATION :
Use clock-wise rule to find the result.

15. ANSWER :
The array dimension is 1
EXPLANATION :
Arrays cannot be passed to functions as arguments and only pointers can be passed, hence the argument which is equivalent to int *arr (this is one of the very few places where [] and *usage are equivalent). The return statement eluates as, sizeof(*it ) sizeof(int), which happens to be equal in this case.

# POINTERS

1. ANSWER :
1 2
EXPLANATION :
The sizeof() operator gives the number of bytes of its operand. The ptr variable is a character pointer, which needs one byte for storing its value (a character), hence sizeof(*ptr) returns a value of 1. Since it needs two bytes to store the address of the character pointer sizeof(ptr) returns 2.

2. ANSWER :
d
Explanation :
The statement (ptr = &s[3]), indicates that the variable ptr is pointing to character 'n'. The statement (str=s), indicates that the variable str is pointing to character 'a'. The expression ++*ptr, indicates that, ptr( pointing to 'n') is incremented by one. The ASCII value of 'n' is 10, which is then incremented to 11. The value of ++*ptr is 11. The expression ++*str, indicates that, str( pointing to 'a') is incremented by one. The ASCII value of 'a' is 97, which is then incremented to 98. The value of ++*str is 98. Now performing (11 + 98 - 9), we get 100, which is the ascii value of 'd', hence we get the above output.

3. ANSWER :
SomeGarbageValue--1
Explanation :
The variable declaration arr[2][2][2], in the first line declares only 2 two-dimensional arrays. But in the statement ptr = arr[2][2][2], you are trying to access the 3rd two-dimensional array (which you are not declared) so it will take some garbage values. If you print *ptr, it will print some garbage value. The statement *q = ***a, assigning the starting address of array arr. If you print *qtr, it will print first element of array arr.

4. ANSWER :
100, 100 - 100, 1
114 - 106 - 102 - 2
Explanation :
The given array is a 3-dimensional array. Let us assume the initial address of the array is 100, which means the given array values are stored in contiguous memory locations. Thus, the first print() function a, '*a' prints the address of first element of the array, and the indirection operator '***a' gives the value of the first location of the array. The second print() function a+1 increases in the third dimension and thus points to value at the address 114, 'a+1' increments in second dimension and thus points to 106, '*a+1' increments the first dimension and thus points to 104 and '**a+1' gets the value at the second location, since first location is incremented by 1) and points to the value in the second location (i.e., 2), hence you get the above output.