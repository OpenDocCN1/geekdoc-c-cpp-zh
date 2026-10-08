# Passing a One-Dimensional Array to a Function

| sales[0] | sales[1] | sales[2] | sales[3] | sub | removed from memory after the for loop on Lines 14 through 19 | removed from memory after the for loop on Lines 23 through 27 |
|---|---|---|---|---|---|---|n| 123.67 | 350.89 | 569.0 | 224.38 | 6 | 4 | 4 |

Figure 11-18 Desk-table after the for loop on Lines 23 through 27 ends

Finally, the computer system("pause"); and return 0; statements on Lines 29 and 30. When the program ends, the computer removes the array from its internal memory.

# Passing a One-Dimensional Array to a Function

Figure 11-19 shows a modified version of the XYZ Company's sales program. In the modified, the main void function displayArray-The changes to the original code (shown earlier in Function prototype, are also shown in Figure 11-19. Study closely the displayArray function prototype, function call, and function header. The call, which appears on Lines 26, provides items of information to the displayArray function: the sales array and the number of elements in the array. You pass an array by including the array's name-in this case, use sales-the actual argument. As you know, variables can be passed to a function by value or by reference. Unless specified, scalar variables in C++ are passed by value. To pass a scalar variable by reference, you will need to include the address-of (&) operator before the formal parameter name in the receiving function. You also need to include the address-of (&) operator in the receiving function prototype. Unlike scalar variables, arrays in C++ are passed by reference rather than value; because it is more efficient to pass arrays in that manner. Since many arrays are large, passing an array by value would consume a great deal of the computer's memory and time, because the computer would need to duplicate the array in the receiving function's formal parameter. Passing an array by reference allows the function to pass the address of only the first array element. Because elements are stored in contiguous locations in memory, the computer can use the address to locate the remaining elements in the array. Given that arrays are passed automatically by reference, you do not include the address-of (&) operator before the name in the function header, as do when passing scalar variables by reference. You also do not include that you are passing an array by simply entering the formal parameter's data type and name, followed by an empty set of square brackets, in the receiving function and in its prototype.

> You learned about passing by value and by reference in Chapters 9 and 10.

(Recall that the formal parameter's name is optional in the prototype. Therefore, you could also write the function prototype in Figure 11-19 as double [])

433