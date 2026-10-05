# F.12. SUMMARY

Notice that the stack and heap segments grow toward each other. Deep recursion can consume considerable amount of stack space. An improperly written recursive function, for example, one that omits the base case and exhibits "infinite" recursion, will cause the stack to collide with the heap. Modern operating systems will terminate a process that consumes all of its stack space, but on some embedded systems this stack overflow may go undetected. A program that allows for dynamic memory, especially a program with memory leaks, may cause the heap to collide with the stack. In either case the executing program does not have enough memory available to satisfy its needs, so the operating system will terminate the program's execution.

# F.12 Summary

+   - An array collects of homogeneous data values.
- An array references the starting address of a chunk of contiguous memory that holds the array's elements.
- The type of values contained by an array and the number values the array can hold are specified when the array is declared; for example,
`double list[20];
- An element of an array is accessed via a non-negative integer index using the [] operator; for example,
`v[3] = 4.1;`
The index of the desired element is placed within the square brackets.
- The first element in an array is at index zero. If the array contains n elements, the last element is at $n-1$.
- For non-dynamic arrays, an array's size must be specified when it is declared; for example,
`int numbers[10]; // numbers holds 10 integers`
- An array's contents may be initialized when the array is declared, as in
`int arr[] = { 2, 4, 6, 8 };`
- Any expression compatible with integer can be placed within the [] operator. Literals, variables, and expressions can be used. The compiler will issue an error if a floating-point expression is used within the square brackets.
- A `for` loop is a convenient way to traverse the contents of an array.
- Like other variables, an array variable can be local, `static` local, or global.
- An array can be passed to a function. The actual parameter passed to the function is a pointer to the first element of the array. Ordinarily, the caller must pass an additional parameter specifying the number of elements within the array, since an array does not keep track of its own size.
- If a function is not supposed to modify the contents of an array, best programming practices insist the array parameter be declared `const`.