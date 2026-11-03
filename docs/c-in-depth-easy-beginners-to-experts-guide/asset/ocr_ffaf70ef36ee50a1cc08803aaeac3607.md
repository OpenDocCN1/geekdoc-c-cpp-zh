The #include directive instructs the C Preprocessor to find the text file “stdio.h”. The name itself means “standard input and output” and the “.h” means it is a header file rather than a C source file (which have the “.c” suffix). It is a text file and may be viewed with any text editor.

# **Comments –**

Comments are placed within /* and */ character sequences and may span any number of lines.

# **Main -**

The main function is most important. This defines the point at which your program starts to execute. If you do not write a main function your program will not run (it will have no starting point). In fact, it won't even compile.

# **Braces –**

C uses the brace character “{” to mean “begin” and “}” to mean “end”. They are much easier to type and, after a while, a lot easier to read.

# **Printf () –**

The printf function is the standard way of producing output. The function is defined within the Standard Library, thus it will always be there and always work in the same way. This example shows that printf and scanf share the same format specifiers.

When presented with “%i” they both handle integers. scanf, because it is a reading function, reads integers from the keyboard. printf, because it is a writing function, writes integers to the screen. Expressions Note that C is quite happy to calculate “a-b” and print it out as an integer value. It would have been possible, but unnecessary, to create another variable “c”, assign

The printf function writes output to the screen. When it meets the format specifier %i, an integer is output.

# **Scanf() -**

The scanf function is the “opposite” of printf. Whereas printf produces output on the screen, scanf reads from the keyboard. The sequence “%i” instructs scanf to read an integer from the keyboard. Because “%i %i” is used two integers will be read. The first value typed placed into the variable “a”, the second into the variable “b”. The scanf function reads input from the keyboard. When it meets the format specifier %i the