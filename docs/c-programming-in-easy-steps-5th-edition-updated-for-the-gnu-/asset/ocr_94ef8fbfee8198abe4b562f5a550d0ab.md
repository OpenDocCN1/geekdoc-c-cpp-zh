# Reading & writing entire files

Whole files can be read with the fread() function and written with the fwrite() function. Both these functions take the same four arguments. The first is a char variable where the text can be stored. The second argument specifies the size of the chunks of text to read or write at a time – normally this will be 1. The third argument specifies the total number of characters to read or write, and the fourth argument is a file pointer to the file to work with.

The fread() function returns the number of objects it has read, counting characters, spaces, and newlines as one object each. Similarly, fwrite() returns the number of objects it has written.

+   1. Begin a new program with a preprocessor instruction to include the standard input/output library functions
+      `#include <stdio.h>`

![](bbox=[0.1, 0.68, 0.22, 0.78])

readwrite.c

+   1. Add a main function that declares two file pointers, a character array variable, and an integer variable
+   ```c
+   int main()
+   {
+   FILE *orig_ptr
+   ; FILE *copy_ptr
+   ; char buffer[1000] ;
+   int num ;
+   }
+   ```

+   3. Next, in the main function block, attempt to open an existing local file to read and another file to write to
+   ```c
+   orig_ptr = fopen ( "original.txt" , "r" ) ;
+   copy_ptr = fopen( "copy.txt" , "w" ) ;
+   ```