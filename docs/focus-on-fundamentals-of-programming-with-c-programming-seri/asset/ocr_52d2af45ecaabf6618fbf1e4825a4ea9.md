# Extra Credit

For extra credit you will need to convert your text aligner program into a text formatter program, `format.c`. This is a program that outputs the words of the text on lines that are both left and right justified. Fortunately, we've modularized our program so well that this only involves adding a single new function, `fmt()`, which inserts additional spaces between words in `lbuf` to achieve full justification. This function should be called just prior to sending `lbuf` to standard output.

Each of your programs should run on the file: `getty.txt`.

![](bbox=[0.12, 0.27, 0.93, 0.75])

Remember that the `main()` function should appear as the first function in the program. Be sure to use function prototypes for each of the functions that are used in your program.