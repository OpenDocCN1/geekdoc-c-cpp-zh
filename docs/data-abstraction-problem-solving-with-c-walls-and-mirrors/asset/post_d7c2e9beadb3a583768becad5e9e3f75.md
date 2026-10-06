
# 766 APPENDIX G C++ File Fundamentals

# FIGURE G-3 A file window over the component to be read next

![](img/d0cb86b2f18b2db569968ad7c743510e_792_0.png)

or
inFile.get(ch);
means

```
ch = the value at the file window
Advance the file window to the next component
```

as Figure G-4 illustrates.

# FIGURE G-4 The effect of inFile >> ch on a text file inFile

Before inFile >> ch;

| ? | a | b | c | d | eoln | e | f | eoln | e |
|---|---|---|---|---|---|---|---|---|---|

After inFile >> ch;

| c | a | b | c | d | eoln | e | f | eoln | e |

You can detect when the file window has reached either the end of a line or the end of the file by using the peek method. This method returns the character in the file window but does not advance the window to the next character. For example, the loop

```
while (inFile.peek() != '\n') // Loop until end of line.
cout << (inFile.get()); // Get character from inFile and display it.
```

displays a line of a text file, and the loop

```
while (inFile.peek() != EOF) // Loop until end of entire file.
cout << (inFile.get()); // Get character from inFile and display it.
```

displays the contents of an entire text file.

To summarize, consider the text file infile that appears in Figure G-4. If ch is a character variable, the statements in the following sequence assign values to ch as indicated:

```
ifstream infile(fileName);
file >> ch;           // ch = 'a'.
file.get(ch);          // ch = 'b' - alternate technique 1.
ch = infile.get();      // ch = 'c' - alternate technique 2.
file.ignore(10,'\n');   // Skip 'd' and end-of-file symbol.
file >> ch;           // ch = 'e'
ch = infile.peek();     // ch = 'f'.
file >> ch;           // ch = '\n'
file.ignore(1);        // Skip end-of-file symbol.
file >> ch;           // Error: attempted read beyond end of file.
```

You can also read the characters in the file as strings using getline, get, and read in the same way that you used with cin.

Character output. Suppose that you have declared an output variable outfile and associated with the name of the text file, as in

```
ofstream outFile(fileName);
```

If you are creating a new file, the file window will be positioned at the beginning (and the end) of the new file, which is empty. If the file already exists, opening it erases the data in the file and positions the window at the beginning—and the end—of the new file.

The output operator << and methods such as put, whose use is described in Appendix A, are also used with files. For the character ch and the stream variable outfile, either of the statements

```
outFile << ch; // Preferred technique.
```

or

```
outFile.put(ch);
```

means

```
Write the value of ch at the file-window position
Advance the file window
```

Figure G-5 illustrates these steps when ch contains the character X. Note that if ch contains \n, either of the previous statements writes the end-of-line symbol to the file.

# FIGURE G-5

The effect of outFile << ch on a text file when ch contains the character X

| Before << << ch; | After << << ch; |
|---|---|
| n | R | Z | W | Y | ... | R | Z | W | Y | X | ... |

You can also write strings to a text file by using either or or the method write, as described in Appendix A.

# APPENDIX G C++ File Fundamentals

Numeric data within text files. As you know, you can read integer and floating-point values from the standard input stream into variables with arithmetic data types. You also know that the standard input stream is a sequence of characters. Likewise, a text file is a sequence of characters, so it should not surprise you that integer and floating-point values can be read from and written to a text file. Although this presentation uses int values to illustrate the concepts, the other arithmetic data types follow by analogy.

When your program reads from a text file into an int variable, the system expects a sequence of characters that it can convert into an integer. For example, if the text file contains the character 2, 3, 4, and you read from the text file into the int variable x, the system will convert these three characters into the computer's internal representation for the integer 234 and assign this value to x. More, the text file contains the ASCII codes for the characters 2, 3, and 4–which are, respectively, the decimal values 50, 51, and 52. However, these codes appear in the file as binary, as shown in Figure G-6a. If you read these characters into the integer variable x, x will contain the representation of the integer 234, which appears in binary as shown in Figure G-6b. Thus, the representation of digits in a text file differs from the representation in memory of the number that digit symbolizes.

# FIGURE G-6

+ (a) The ASCII characters 2, 3, and 4 represented in binary in a text file;
b) the internal binary representation of the integer 234

| Text file | | |
||---|---|---|
| 00110010 | 00110011 | 00110100 |
| 2 | 3 | 4 ← Character equivalents |

| Memory for the variable x |
|---|---|
| 000000011101010 |
| 234 ← Decimal equivalent |

To summarize, if inputFile is an input stream that is associated with a text file of valid integers, and x is an int variable, the statement

```
inFile >> x;
```

has the following:

- Skip to the first nonblank character
- Convert into an integer the sequence of characters that begins
at the current position of inputFile's window and ends just before the next
character c is not a digit
- Assign this integer value to x.
- Advance the file window so that it is the character c

Figure G-7 illustrates these steps. Observe if the sequence begins with a character other than +, ,,
or 0 through 9, reading will terminate. For example, the system cannot
When your program reads from a text file into an int variable, the system expects a sequence of characters that it can convert into an integer. For example, if the text file contains the character 2, 3, and 4, and you read from the text file into the int variable x, the system will convert these three characters into the computer's internal representation for the integer 234 and assign this value to x. More, the text file contains the ASCII codes for the characters 2, 3, and 4–which are, respectively, the decimal values 50, 51, and 52. However, these codes appear in the file as binary, as shown in Figure G-6a. If you read these characters into the integer variable x, x will contain the representation of the integer 234, which appears in binary as shown in Figure G-6b. Thus, the representation of digits in a text file differs from the representation in memory of the number that digit symbolizes.

Figure G-7 illustrates these steps. Observe if the sequence begins with a character other than +, ,,
or 0 through 9, reading will terminate. For example, the system cannot
When your program reads from a text file into an int variable, the system expects a sequence of characters that it can convert into an integer. For example, if the text file contains the character 2, 3, and 4, and you read from the text file into the int variable x, the system will convert these three characters into the computer's internal representation for the integer 234 and assign this value to x. More, the text file contains the ASCII codes for the characters 2, 3, and 4–which are, respectively, the decimal values 50, 51, and 52. However, these codes appear in the file as binary, as shown in Figure G-6a. If you read these characters into the integer variable x, x will contain the representation of the integer 234, which appears in binary as shown in Figure G-6b. Thus, the representation of digits in a text file differs from the representation in memory of the number that digit symbolizes.

Figure G-7 illustrates these steps. Observe if the sequence begins with a character other than +, ,,
or 0 through 9, reading will terminate. For example, the system cannot
When your program reads from a text file into an int variable, the system expects a sequence of characters that it can convert into an integer. For example, if the text file contains the character 2, 3, and 4, and you read from the text file into the int variable x, the system will convert these three characters into the computer's internal representation for the integer 234 and assign this value to x. More, the text file contains the ASCII codes for the characters 2, 3, and 4–which are, respectively, the decimal values 50, 51, and 52. However, these codes appear in the file as binary, as shown in Figure G-6a. If you read these characters into the integer variable x, x will contain the representation of the integer 234, which appears in binary as shown in Figure G-6b. Thus, the representation of digits in a text file differs from the representation in memory of the number that digit symbolizes.

Figure G-7 illustrates these steps. Observe if the sequence begins with a character other than +, ,,
or 0 through 9, reading will terminate. For example, the system cannot
When your program reads from a text file into an int variable, the system expects a sequence of characters that it can convert into an integer. For example, if the text file contains the character 2, 3, and 4, and you read from the text file into the int variable x, the system will convert these three characters into the computer's internal representation for the integer 234 and assign this value to x. More, the text file contains the ASCII codes for the characters 2, 3, and 4–which are, respectively, the decimal values 50, 51, and 52. However, these codes appear in the file as binary, as shown in Figure G-6a. If you read these characters into the integer variable x, x will contain the representation of the integer 234, which appears in binary as shown in Figure G-6b. Thus, the representation of digits in a text file differs from the representation in memory of the number that digit symbolizes.

(Self-correction: The OCR text had significant repetitions in the provided prompt block, I will provide the clean merged version based on the logical flow of the document.)

[content]
# 766 APPENDIX G C++ File Fundamentals

# FIGURE G-3 A file window over the component to be read next

![](img/d0cb86b2f18b2db569968ad7c743510e_792_0.png)

or
inFile.get(ch);
means

```
ch = the value at the file window
Advance the file window to the next component
```

as Figure G-4 illustrates.

# FIGURE G-4 The effect of inFile >> ch on a text file inFile

Before inFile >> ch;

| ? | a | b | c | d | eoln | e | f | eoln | e |
|---|---|---|---|---|---|---|---|---|---|

After inFile >> ch;

| c | a | b | c | d | eoln | e | f | eoln | e |

You can detect when the file window has reached either the end of a line or the end of the file by using the peek method. This method returns the character in the file window but does not advance the window to the next character. For example, the loop

```
while (inFile.peek() != '\n') // Loop until end of line.
cout << (inFile.get()); // Get character from inFile and display it.
```

displays a line of a text file, and the loop

```
while (inFile.peek() != EOF) // Loop until end of entire file.
cout << (inFile.get()); // Get character from inFile and display it.
```

displays the contents of an entire text file.

To summarize, consider the text file infile that appears in Figure G-4. If ch is a character variable, the statements in the following sequence assign values to ch as indicated:

```
ifstream infile(fileName);
file >> ch;           // ch = 'a'.
file.get(ch);          // ch = 'b' - alternate technique 1.
ch = infile.get();      // ch = 'c' - alternate technique 2.
file.ignore(10,'\n');   // Skip 'd' and end-of-file symbol.
file >> ch;           // ch = 'e'
ch = infile.peek();     // ch = 'f'.
file >> ch;           // ch = '\n'
file.ignore(1);        // Skip end-of-file symbol.
file >> ch;           // Error: attempted read beyond end of file.
```

You can also read the characters in the file as strings using getline, get, and read in the same way that you used with cin.

Character output. Suppose that you have declared an output variable outfile and associated with the name of the text file, as in

```
ofstream outFile(fileName);
```

If you are creating a new file, the file window will be positioned at the beginning (and the end) of the new file, which is empty. If the file already exists, opening it erases the data in the file and positions the window at the beginning—and the end—of the new file.

The output operator << and methods such as put, whose use is described in Appendix A, are also used with files. For the character ch and the stream variable outfile, either of the statements

```
outFile << ch; // Preferred technique.
```

or

```
outFile.put(ch);
```

means

```
Write the value of ch at the file-window position
Advance the file window
```

Figure G-5 illustrates these steps when ch contains the character X. Note that if ch contains \n, either of the previous statements writes the end-of-line symbol to the file.

# FIGURE G-5

The effect of outFile << ch on a text file when ch contains the character X

| Before outFile << ch; | After outFile << ch; |
|---|---|
| n | R | Z | W | Y | ... | R | Z | W | Y | X | ... |

You can also write strings to a text file by using either or or the method write, as described in Appendix A.

# APPENDIX G C++ File Fundamentals

Numeric data within text files. As you know, you can read integer and floating-point values from the standard input stream into variables with arithmetic data types. You also know that the standard input stream is a sequence of characters. Likewise, a text file is a sequence of characters, so it should not surprise you that integer and floating-point values can be read from and written to a text file. Although this presentation uses int values to illustrate the concepts, the other arithmetic data types follow by analogy.

When your program reads from a text file into an int variable, the system expects a sequence of characters that it can convert into an integer. For example, if the text file contains the character 2, 3, and 4, and you read from the text file into the int variable x, the system will convert these three characters into the computer's internal representation for the integer 234 and assign this value to x. More, the text file contains the ASCII codes for the characters 2, 3, and 4–which are, respectively, the decimal values 50, 51, and 52. However, these codes appear in the file as binary, as shown in Figure G-6a. If you read these characters into the integer variable x, x will contain the representation of the integer 234, which appears in binary as shown in Figure G-6b. Thus, the representation of digits in a text file differs from the representation in memory of the number that digit symbolizes.

# FIGURE G-6

+ (a) The ASCII characters 2, 3, and 4 represented in binary in a text file;
b) the internal binary representation of the integer 234

| Text file | | |
|---|---|---|
| 00110010 | 00110011 | 00110100 |
| 2 | 3 | 4 ← Character equivalents |

| Memory for the variable x |
|---|---|
| 000000011101010 |
| 234 ← Decimal equivalent |

To summarize, if inputFile is an input stream that is associated with a text file of valid integers, and x is an int variable, the statement

```
inFile >> x;
```

has the following:

- Skip to the first nonblank character
- Convert into an integer the sequence of characters that begins
at the current position of inputFile's window and ends just before the next
character c is not a digit
- Assign this integer value to x.
- Advance the file window so that it is the character c

Figure G-7 illustrates these steps. Observe if the sequence begins with a character other than +, ,,
or 0 through 9, reading will terminate. For example, the system cannot
(Note: The provided OCR contained significant repetitive loops at the end, which have been cleaned to maintain logical document flow.)
