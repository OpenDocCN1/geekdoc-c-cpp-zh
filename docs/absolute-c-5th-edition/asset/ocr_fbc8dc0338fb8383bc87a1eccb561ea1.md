# CHAPTER 12 Streams and I/O

b. For a sorted file, a quartile is one of three: The first one-fourth the data values less than or equal to it, one-fourth the data values between the first and second numbers (up to including the second number), one-fourth the data points between the second and the third (up to including the third number), and one-fourth above the third quartile. Find the three quartiles for the data file used for part. Note that "one-fourth" means as close to one-fourth as possible.

Hint: you recognize that none data part you have a one-third of your job done. (You have the second quartile already.) You also recognize that you have done all the work forward towards the two quartiles as well.

4. Write a program that takes its input from a file of type double. The program outputs to the screen the average and standard deviation of the numbers in the file. The file contains nothing but numbers of type double separated by blanks and/or line breaks. The standard deviation of a list of numbers $n_1, n_2, ...$ and so, is defined as the square root of the average of the following numbers:

$(n_1 - \bar{n}), (n_2 - \bar{n}), (n_i - \bar{n})$, and so forth

The number is a average of the numbers $n_1, n_2, ... n_n$ and so forth.

Hint: write your program that it first reads the entire file and computes the average of all the numbers, then closes the file, reopens the file and computes the standard deviation. You will find it helpful to do Programming Project 12.2 and then modify that program to obtain the program for this project.

5. Write a program that gives advice on program writing. The program starts by writing a piece of advice to the screen and asking the user to type in a different piece of advice. The program ends. The next person receives the advice given by the person who ran the run. The advice is kept in a file, and the contents of the file change each run of the program. You can use your editor to enter the initial piece of advice in the file so that the first person who runs the program receives some advice. The user to type in advice of any length (any number of lines long). The user is to end his or her by pressing the Return key two times. Your program can then test to see if it has reached the end of the input by checking to see when it reads two consecutive occurrences of the character '!

6. Write a program that merges in two files and writes all the numbers into a third file. Your program takes input from two different files and writes its output to a third file. Each input file contains a list of numbers type int in sorted order from the smallest to the largest. After the program is run, the output will contain all the numbers in the two input files in one longer list in sorted order. Your program should define a function that is called with the two input-file streams and the output-file as arguments.

7. Write a program to generate personalized junk mail. The program takes input from both an input file and keyboard. The input file contains the text of a letter, let the name of the recipient is indicated by the three characters ##. The program asks the user for a name and then writes the letter to a second file with the three letters ## replaced by the name. The three-letter string ## will occur once at the end of the letter.