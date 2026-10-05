
46. b

**Explanation:** The break statement can also be used in loops.

47. c

**Explanation:** It is a practice question. The explanation is not required.

48. b

**Explanation:** The goto statement transfers the control of execution from the current instruction to the labelled instruction. Its step size is not fixed. The goto statements are not frequently used in C. It makes the control flow of a program logically complex which is difficult to understand. It is not a good practice using goto in a program.

49. b

**Explanation:** Not required.

50. d

**Explanation:** In a given program, from main(), it is tried to use the instruction of a different function without calling the function. It is not possible to access the function body without calling it. The function gets pushed into the memory area (stack) then only it can get used. Here, the compiler throws an error- label1 is undefined. If we want to use a label with goto, it must be local to a function.

51. b

**Explanation:** It works fine in gcc but in Turbo C it throws an error. GNU C supports the nesting of functions.

52. d

**Explanation:** Given a[2][2][3], 2D arrays of size 2x3.

| a[0] | 5 | 6 | 7 |
|---|---|---|---|
| | 1000 | 1004 | 1008 |
| a[1] | 8 | 9 | 10 |
| | 1012 | 1016 | 1020 |
| a[2] | 11 | 12 | 13 |
| | 1036 | 1040 | 1044 |

![](img/192d581e3a01f0e6c194cfc2ff02d9f1_120_0.png)

Suppose we want to access an element a[1][1][2]. In 3D, a[1] means skipping one 2DArray and a[1] (or *(a+1)), highlighted '*' means selecting the row in selected 2D array, a[1][1][2] means skipping 2 column.

(i)*(a[i])->*(i+1)); I means skipping the first array and the inside *(close to a) means selecting the second array[i]. Second ** (middle) means selecting the particular row in array[i]. The outside means selecting the particular element without skipping column. (iv)*(a[i]*2)->*(i+1)*2); I means skipping 2DArray and inside means a particular array. Second ** (middle) means selecting the row without skipping element a[i]:0). 2 means skipping the particular element in selected row, and inside selecting particular element. It is equivalent to a[i][0][2] and returns 3.

## 53. c

**Explanation:** Refer explanation of question 52, we can directly access the address using '*' operator without skipping the column or row. Like x = &a[1][1][2] directly get the address 1044 and we can access element at 1044 by doing *(1040). The pointer variable 'y' holds address 1000, we can directly access the value at 1000 using *1000. Hence, the program will return *1044 and *1000 that value is 13 and 5.

x : 1044 y : 1000

## 54. a

**Explanation:** a[2][2][3] means we have two 2D arrays of size 2x3. As we discussed in the explanation of question 52, a[1][2] means skipping 1D array and then skipping 2 rows in the selected array. Here, each 2D array contains only two rows if we skip two rows, we are getting out of the array space. The garbage value will get printed. a[2][1][0], 2 means skipping two 2D arrays. We are having only 2D arrays, we are trying to access the address out of the array space. Hence, the garbage will get printed.

**Note:** It will not throw an error, because the addresses outside the array space are also readable and garbage will get returned.

## 55. b

**Explanation:** Refer to explanation of question 25.

At line 4, (*int*)p+2; we are again converting the character pointer to an integer type. Now step size becomes 4 which is the same as the integer pointer step size. It is similar to a[2].

## 56. The number of elements in a given array is 16.

**Explanation:** int number_of_elements = sizeof(a)/sizeof(a[0]);

## 57. Nil

**Explanation:**

| *str1[] | | str2[5][5] | | **str3 | |
|---|---|---|---|---|---|---|---|
| str1: | | 'h' | 'e' | 'l' | 'o' | '\0' | It is a double character |
| 1000 | 2000 | 3000 | 4000 | 'T' | 'n' | 'i' | 't' | '\0' | pointer that is capable of |
| 100 | 104 | 108 | 112 | 'T' | 'o' | 'v' | 'c' | '\0' | storing address of |
| | | | | | 'g' | 'r' | 'e' | 'a' | 't' | character pointer. |
| hello/0 | India/0 | love/0 | great/0 | '\0' | str3 = str2//possible |
| 1000 | 2000 | 3000 | 4000 | | str3 = str1//possible |

Figure 3.7: Representation of char pointer in text and stack area

All three types of declarations are interchangeably used by keeping a few conditions in mind. (i) Base address of an array cannot be updated. The table below table briefly describes the possible assignment operations with these three types of declarations.

| str declarations (column) | | | |
|---| *str[*]; | str5[5][5]; | **str; |
|---|---|---|---|---|
| Possible str-*&var; | x | ✓ | x = invalid assignment |
| assignment *str&var; | ✓ | x | Valid assignment |
| operations (row) | **str; | ✓ | ✓ |

Table 3.1: Assignment for str with given declarations

## 58. c

**Explanation:**

| (i) char *ptr[] = {"hello\0","India\0","love\0","great\0"}; | | |
| hello/0 | India/0 | love/0 | great/0 | 1000 | 2000 | 3000 | 4000 |
| 1000 | 2000 | 3000 | 4000 | 100 | 104 | 108 | 112 |
| *ptr[1]; | **ptr; | 508 | (iii) p = ptr; | (ii) char **ptr[] = {str+1, str+2, str+3}; |
|---|---|---|---|---|
| ->*108; | ->*508; | 700 | (iv) p = ptr2; | 100 | 104 | 108 |
| ->*3000; | ->*104; | | 500 | 504 | 108 |
| String at address | 2000; | step size is 4 (pointer) | | 512 |
| returned by printf | returned by printf | | p = 508; |
| using %s; | using %s; | | |
| love | India | | |

## 59. d

**Explanation:** The variable assignment is step as the previous question, there is only a change in step (iv), here's p = p+3.

```
p = p+3;
(iv) p = 3;
p = 500;
#step size is 4 (pointer)
p=512;
```
```
--> (****)2;
--> (*ptr[1]+'a';
--> (**12)+2;
--> (*ptr+1))'a';
--> 4000/2;
--> (*500+1))'a';
--> 500/1;
--> (*504) + 1;
/step size is 1
String at address 4002 will
returned by prnt using
%,
O/p: cat
--> 3000/1; step
String at address 4000/1;
returned by prnt using
O/p: ove
```
![](img/192d581e3a01f0e6c194cfc2ff02d9f1_123_0.png)

## 60. c

**Explanation:** When a user requests dynamic allocation, the C program requests memory. If the memory is available, the memory manager allocates the memory to the program. If the system is too busy, the memory manager can deny the request to allocate memory for the program. Here, in a given program the memory is allocating dynamically in infinite loop without deallocating(free()). The main memory (RAM) gets completely allocated to our program, the heap overflows and the system (having Unix operating system) hangs. If we deallocate the memory in each iteration, the heap will not overflow, the system will not hang, just the hello 10 will printed infinite time. See the following program:

```c
#include<stdio.h>
#include<stdlib.h>
int main() {
    while (1) {
        int *p = (int *)malloc(sizeof(int));
        *p=10;
        printf("hello %d", *p);
        free(p);
        p=NULL; // to avoid dangling pointer (Group1, Question 7 explanation)
    }
    return 0;
}
```
