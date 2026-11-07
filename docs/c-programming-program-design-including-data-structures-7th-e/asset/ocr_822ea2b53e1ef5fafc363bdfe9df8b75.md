# **PROGRAMMING EXAMPLE:** Text Processing

![](bbox=[0.072, 0.187, 0.131, 0.258])

**(Line and letter count)** Let us now write a program that reads a given text, outputs the text as is, and also prints the number of lines and the number of times each letter appears in the text. An uppercase letter and a lowercase letter are treated as being the same; that is, they are tallied together.

Because there are 26 letters, we use an array of 26 components to perform the letter count. We also need a variable to store the line count.

The text is stored in a file, which we will call `textin.txt`. The output will be stored in a file, which we will call `textout.out`.

**Input**  A file containing the text to be processed.

**Output**  A file containing the text, number of lines, and the number of times a letter appears in the text.

+   - PROBLEM
+   - ANALYSIS
+   - AND
+   - ALGORITHM
+   - DESIGN

Based on the desired output, it is clear that we must output the text as is. That is, if the text contains any whitespace characters, they must be output as well. Furthermore, we must count the number of lines in the text. Therefore, we must know where the line ends, which means that we must trap the newline character. This requirement suggests that we cannot use the extraction operator to process the input file. Because we also need to perform the letter count, we use the `get` function to read the text.

Let us first describe the variables that are necessary to develop the program. This will simplify the discussion that follows.

# Variables

We need to store the line count and the letter count. Therefore, we need a variable to store the line count and 26 variables to perform the letter count. We will use an array of 26 components to perform the letter count. We also need a variable to read and store each character in turn, because the input file is to be read character by character. Because data is to be read from an input file and output is to be saved in a file, we need an input stream variable to open the input file and an output stream variable to open the output file. These statements indicate that the function `main` needs (at least) the following variables:

```
int lineCount;       //variable to store the line count
int letterCount[26]; //array to store the letter count
char ch;             //variable to store a character
ifstream infile;     //input file stream variable
ofstream outfile;    //output file stream variable
```

In this declaration, `letterCount[0]` stores the A count, `letterCount[1]` stores the B count, and so on. Clearly, the variable `lineCount` and the array `letterCount` must be initialized to 0.