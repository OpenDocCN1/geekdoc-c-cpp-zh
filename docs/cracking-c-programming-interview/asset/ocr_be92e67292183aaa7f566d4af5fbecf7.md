40.

# Explanation:

In the given program, we are defining macro max with macro value 5 and int with macro value arr1[max] and these marco will be multiplied by their values in pre-processor phase; we are also defining arr2 as an array of 5 element of type character. The pre-processed code will look

```
#include<stdio.h>
main() {
  int arr1[] = {0,1,2,3,4};
  char name[5] = "name";
  printf("%s",arr1[0]);
}
```

After pre-processing compiler will found 'arr1' that is unknown and will raise an error.

41. c

Explanation: In a given program, in function fun(), the string "Hello India" is pointed by 'p' gets stored in the code area which is shared and available to all the functions in a program. Hence, we can access this string through its address from the main function also.

42. d

Explanation: In function foo1() and foo2(), the memory for array 'a' is getting allocated in the local area (stack area) only. After the execution of function foo1() and foo2(), both return the base address of array 'a' and the memory pointed by 'a' will not be available in the main function. At line 4 and line 5 in main(), we are trying to access the unavailable memory, it returns garbage or sometimes the same string can also get returned but never be an error. On the other note, array in foo2() is not null-terminated, if we print 'a' in foo2() with %s, it prints "India<garbage>" till the null character encounters.

43. b

Explanation: The character 'a' has 4 bytes to store its string and we are also giving exactly 4 characters to it, hence, no place for termination character(\0). When we print the array 'a' by printf() using "%s" format specifier, it will print characters until it gets termination character. So, "kink<some garbage value>" gets printed.

44. a

Explanation: In function argument, only pointer gets passed for an array, if we pass array then then also it is treated as a pointer. So,