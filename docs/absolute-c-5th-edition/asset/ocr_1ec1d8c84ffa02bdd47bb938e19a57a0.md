# CHAPTER 5 Arrays

+   - The indexed variables for an array are stored next to each other in the computer’s memory so the array occupies a contiguous portion of memory. When the array is passed as an argument to a function, only the address of the first indexed variable (the one numbered :) is given to the calling function. Therefore, a function with an array parameter usually needs another formal parameter of type int to give the size of the array.

+   - When using a partially filled array, your program needs an additional variable of type int to keep track of how much of the array is used.

+   - To tell the compiler that an array should not be changed by your function, you can insert the modifier const before the array parameter for argument position. An array parameter that is modified with a const is called a constant array parameter.

+   - If you need an array with more than one index, you can use a multidimensional array.

# Answers to Self-Test Exercises

+   1. The statement int a[5]; is a declaration, in which 5 is the number of array elements. The expression a[4] is an access into the array defined by the previous statement. The access is to the element having index 4, which is the fifth (and last) element.

+   2. a. score
   b. double
   c. 5
   d. 0 through 4

+   e. Any of score[0], score[2], score[3], score[4]

+   3. a. One many initializers
   b. Correct. The array size is 4.
   c. Correct. The array size is 4.

+   4. abc
   5. 1.1 2.2 3.3
   1.1 3.3 3.3

(Remember that the indexes start with 0, not 1.)

+   6. 0 2 4 6 8 10 12 14 16 18
   0 4 8 12 16

+   7. The indexed variables of sampleArray are sampleArray[0] through sampleArray[9], but this piece of code tries to fill sampleArray[1] through sampleArray[10]. The index 10 in sampleArray[10] is out of range.