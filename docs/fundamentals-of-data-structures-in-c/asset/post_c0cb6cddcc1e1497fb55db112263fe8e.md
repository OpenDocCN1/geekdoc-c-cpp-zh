
### 5.

ANSWER : Compiler Error: lvalue required.

EXPLANATION : Error is in statement a++. The operand must be an lvalue and may be of any of scalar type for any operator, but array name only when subscripted becomes an lvalue. Simply using an array name is unalterable lvalue.

### 6.

ANSWER :
1 1 1
2 2 2
3 3 3

EXPLANATION : The given array is a 3-dimensional array. Let us assume the initial address of the array is 1000, which means the subsequent array values are stored in contiguous memory locations. The statement "*ptr = p assigns the starting address of the array 'p' to the pointer variable 'ptr'. After execution of the instruction ptr++, the value in ptr becomes 1002, if scaling factor for integer is 2 bytes. The explanation (ptr-p) indicates value in ptr - the value in the starting location of array 'p', (i.e., (1002 - 1000) / (scaling factor) = 1. The expression (ptr++ - *ptr) indicates value in ptr - the value stored in the location pointed by the pointer of ptr. (i.e., the value pointed by 1002) = 1. Hence the output of the first printf() function is 1 1 1. Similarly for all other printf() functions.

### 7.

ANSWER : 1

EXPLANATION : The given array is a 2-dimensional array, which points to its first element and hence the output.

### 8.

ANSWER : A20lo

EXPLANATION : Since a void pointer, (i.e., *vp) is used it can be type casted to any other type pointer. The statement (vp = &ch stores the address of char 'ch' and the next statement prints the value stored in the pointer vp after type casting it to the proper data type pointer, whose output is 'A'. The statement (vp = &j) stores the address of integer 'j' and the next statement prints the value stored in the pointer vp after type casting it to the proper data type pointer, whose output is 20. The statement (vp = cp) stores the address of string 'cp' and the next statement prints the value stored in the pointer vp after type casting it to the proper data type pointer, whose output is 'lo'.

### 9.

ANSWER : ck

EXPLANATION : In this problem we have an array of character pointers 's' pointing to the start of 4 strings. Then we have 'ptr' which is a pointer to a pointer of type char and a variable 'p' which is a pointer to a pointer to a pointer of type char. The variable 'p' holds the initial value of ptr, (i.e., p = s+3). The next statement increments value in p by 1, hence it becomes s+2. In the printf() function the expression *++p is evaluated, thus incrementing the value of p by s+1, then the predecrement operator is executed, and we get s+1 = s. The increment operator now gets the value from the array of s and adds 3 to the starting address. Thus the string is printed from the third position, hence we get the output as 'ck'.

### 10.

ANSWER :

ohn
hn
n

EXPLANATION : Here a string (a pointer to char) is initialized with the value "John". The strlen() function returns the length of the string, thus n has a value 4. The next statement assigns value at the nth location (i.e., '\0') to the first location. Now the string becomes "\0ohn". Now the printf statement prints the string after each iteration it increments its starting position. Loop starts from 0 to 4. The first time x[0] = "\0" hence it prints nothing and pointer value is incremented. The second time it prints from x[1] i.e, "ohn" and the third time it prints "hn" and the last time it prints "n" and the loop terminates.

### 11.

ANSWER : Compiler Error : size of v is Unknown.

EXPLANATION : You can create a variable of type void * but not of type void, since void is an empty data type. In the second line you are creating variable vptr of type void* and v of type void hence an error.

### 12.

ANSWER : 2 5 5

EXPLANATION : The sizeof(str1) is a character pointer so it gives you the size of the pointer variable. The next sizeof(str2) indicates the name of the array whose size is 5 (which includes the '\0' NULL character). The last sizeof("abcd") is similar to the second one, hence you get the above output.

### 13.

ANSWER : 10

EXPLANATION : The variable i is a block level variable and the visibility is inside that block only. But the lifetime of j is lifetime of function so it lives upto the exit of main() function. Since i has its allocated space, "j" prints the value stored in i (since j points to i), hence you get the above output.

### 14.

ANSWER : 0001 - 0002 - 0004

EXPLANATION : The ++ operator when applied to pointers increments address according to their corresponding data-types.

### 15.

ANSWER : Garbage value.

EXPLANATION : The pointer ptr is pointing out of array range of 'an'.

### 16.

ANSWER : 300

EXPLANATION : The pointer points to % since it is incremented twice and again decremented by 2, it points to "%d\n" and 300 is printed.

### 17.

ANSWER : Compiler Error: We cannot apply indirection on type void.

EXPLANATION : Void pointer is a generic pointer type. No pointer arithmetic can be done on it.

### 18.

ANSWER : 4

EXPLANATION : The expressions "a" and -"a" cancels out. The result is as simple as (1+3) = 4.

### 19.

ANSWER : b

EXPLANATION : The expression (ptr++) assigns the first value to ++*(ptr++) expression, and then gets incremented, the expression ++* increments the value in the address stored pointed by the pointer.

### 20.

ANSWER : b

EXPLANATION : There is no difference between the expression ++*(p++) and ++*p++. Note that parenthesis is a visual clue for the reader to see which expression is first evaluated.

### 21.

ANSWER : Some garbage value
0

EXPLANATION : The memory space allocated by the malloc() function is uninitialized, whereas the calloc() function returns the allocated memory space initialized to zeros.

### 22.

ANSWER : 16 16

EXPLANATION : The pointer variables ptr1 and pt2 both refer to the same memory location a. So changes through ptr1 and ptr2 ultimately affects only the value of a.

### 23.

ANSWER : 2 1 4 5 4

EXPLANATION : The expression sizeof(ptr) is similar to sizeof(char*), which is 2. The expression sizeof(*ptr) is similar to sizeof(char), which is 1. The expression sizeof(arr) is size of the character array, which is 5. When sizeof() operator is applied to an array it returns the sizeof the array and it is not the same as the sizeof the pointer variable, since the sizeof(arr) where arr is the character array and the size of array is 5 because the space necessary for the terminating NULL character should also be taken into account.

### 24.

ANSWER : x = 20 y = 10

EXPLANATION : This is one way of swapping two values, using pointers.

### 25.

ANSWER : x = 20 y = 10

EXPLANATION : Just another way of swapping two values, using bitwise operators.

### 26.

ANSWER : 1 1

EXPLANATION : The integer value 257 is stored in the memory as, 00000001 00000001 (in 16 bits), so the individual bytes are taken by casting it to char* and gets printed.

### 27.

ANSWER : 2 1

EXPLANATION : The integer value 258 is stored in the memory as, 00000001 00000010 (in 16 bits), so the individual bytes are taken by casting it to char* and gets printed.

### 28.

ANSWER : 556

EXPLANATION : The integer value 300 in binary notation is, 00000001 00101100. It is stored in memory as, 00101100 00000001. Result of the expression ++*ptr = 2 makes the memory representation as, 00101100 00000010. So the integer corresponding to it is 00000010 00101100 is 556.

### 29.

ANSWER : 0

EXPLANATION : After 'ptr' reaches the end of the string the value pointed by 'str' is '\0'. So the value of 'str' is less than that of 'ch'. So the value of 'ch' is 0.

### 30.

ANSWER & EXPLANATION : If the body of the loop never executes ptr is assigned no address so ptr remains NULL. When 'ptr = 0, may result in problem (which gives rise to runtime error or NULL pointer assignment and terminate the program).

### 31.

ANSWER : Undefined behavior.

EXPLANATION : The second statement results in undefined behavior because it points to some location whose value may not be available for modification. This type of pointer in which the non-availability of the implementation of the referenced location is referenced as 'incomplete types'.

### 32.

ANSWER : 5

EXPLANATION : The output is simple, it divides the two integer pointer values, hence you get the above output.

### 33.

ANSWER : Yes.

EXPLANATION : The pointer ptr will point at the integer in the memory location 0x400.

### 34.

ANSWER : String constant

EXPLANATION : The program suffers no problem and gives the output correctly because the character constants are stored in code/data area and not allocated in the stack, so this doesn't lead to dangling pointers.

### 35.

ANSWER : Garbage values.

EXPLANATION : Both the functions suffer from the problem of dangling pointers. In someFun1() temp is a character array and so the space for it is allocated in heap and is initialized with character string "string". This is created dynamically as the function is called, and is also deleted dynamically on exiting the function so the string data is not available in the calling main() function leading to print some garbage values. The function someFun2() also suffers from the same problem but the problem can be easily identified in this case.

![](img/32da3a4a82d0a65ae37d5228b3ab3ad1_385_0.png)
