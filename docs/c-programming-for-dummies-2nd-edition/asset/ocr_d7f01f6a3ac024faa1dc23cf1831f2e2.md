The source code from Listing 22-7 displays each byte in a file. It uses a 2-digit hexadecimal format, %02X, to represent each byte in the printf() statement at Line 24.

The fgetc() function reads the file one byte at a time in Line 21. To prevent the code from reading beyond the end of the file, this byte is compared with the EOF, or end-of-file, marker at Line 22.

The if decision at Line 26 uses the modulus operator to determine when 16 bytes have been displayed. When true, a newline is output, keeping the display neat and tidy.

Unlike other programs presented in this chapter, Listing 22-7 prompts the user for a filename at Line 10. Therefore, a good possibility exists that you'll see the error message displayed when an improper filename is typed.

Exercise 22-10: Type the source code from Listing 22-7 into your editor. Build the project. Run it using the scores.dat file you created earlier in this chapter, or use the file's own source code listing as the file to view.

Exercise 22-11: Rewrite the source code from Listing 22-7 so that the filename can also be typed at the command prompt as the program's first argument.

![](bbox=[0.15, 0.65, 0.22, 0.8])

+   - Dump is an old programming term. It's an inelegant way to refer to a transfer of data from one place to another without any manipulation. For example, a core dump is a copy of the operating system's kernel (or another basic component) transferred from memory into a file.
+   - The information saved by the fwrite() and read by the fread() functions is binary — effectively, the same information that's stored in memory when you assign a value to an int or a float or another C variable type.
+   - As long as you get the order correct, you can use fwrite() and fread() to save any data to a file, including full arrays, structures, and what-have-you. But if you read the information out of sequence, it turns into garbage.

# Random File Access

Random file access has nothing to do with random numbers. Rather, the file can be accessed at any point hither, thither, and even yon. It's like watching streaming video as opposed to broadcast TV: You can start reading the file at any point, fetching or putting whatever information wherever you need it.