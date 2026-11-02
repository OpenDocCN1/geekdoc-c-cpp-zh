
### Be able to process text in files.

- When reading a string with the >> operator, the white space between words is consumed.
- You can get individual characters from a stream and unget the last one.
- You can read a line of input with the getline function and then process it further.

![](img/d61019b035dd82beb581604273c0ee6b_454_0.png)

### Write programs that neatly format their output.

- Use the setw manipulator to set the width of the next output.
- Use the fixed and setprecision manipulators to format floating-point numbers with a fixed number of digits after the decimal point.

![](img/d61019b035dd82beb581604273c0ee6b_454_1.png)

### Convert between strings and numbers.

- Use an istringstream to convert the numbers inside a string to integers or floating-point numbers.
- Use an ostringstream to convert numeric values to strings.

![](img/d61019b035dd82beb581604273c0ee6b_454_2.png)

### Process the command line arguments of a C++ program.

- Programs that start from the command line can receive the name of the program and the command line arguments in the main function.

![](img/d61019b035dd82beb581604273c0ee6b_454_3.png)

### Develop programs that read and write binary files.

- You can access any position in a random access file by moving the file pointer prior to a read or write operation.

![](img/d61019b035dd82beb581604273c0ee6b_454_4.png)

## REVIEW EXERCISES

**R8.1** When do you open a file as an `ifstream`, as an `ofstream`, or as an `fstream`? Could you simply open all files as an `fstream`?

**R8.2** What happens if you write to a file that you only opened for reading? Try it out if you don't know.

**R8.3** What happens if you try to open a file for reading that doesn't exist? What happens if you try to open a file for writing that doesn't exist?

**R8.4** What happens if you try to open a file for writing, but the file or device is write-protected (sometimes called read-only)? Try it out with a short test program.

**R8.5** How do you open a file whose name contains a backslash, such as `c:\temp\output.dat`?

**R8.6** Why are the `in` and `out` parameter variables of the `encrypt_file` function in Section 8.5 reference parameters and not value parameters?

**R8.7** Give an output statement to write a date and time in ISO 8601 format, such as

`2011-03-01 09:35`

Assume that the date and time are given in five integer variables year, month, day, hour, minute.

**R8.8** Give an output statement to write one line of a table containing a product description, quantity, unit price, and total price in dollars and cents. You want the columns to line up, like this:

| Item | Qty | Price | Total |
|---|---|---|---|
| Toaster | 3 | $29.92 | $89.85 |
| Hair Dryer | 1 | $24.95 | $24.95 |
| Car Vacuum | 2 | $19.99 | $39.98 |

**R8.9** How can you convert the string `"3.14"` into the floating-point number 3.14? How can you convert the floating-point number 3.14 into the string `"3.14"`? Give two ways.

**R8.10** What is a command line? How can a program read its command line?

**R8.11** If a program `woozle` is started with the command

`woozle -DNAME=Piglet -I\eyyore v heff.cpp a.cpp lump.cpp`

what is the value of `argc`, and what are the values of `argv[0]`, `argv[1]`, and so on?

**R8.12** What is the difference between sequential access and random access?

**R8.13** What is the difference between a text file and a binary file?

**R8.14** What are the get and put positions in a file? How do you move them? How do you tell their current positions?

**R8.15** What happens if you try to move the get or put position past the end of a file? What happens if you try to move the get or put position of `cin` or `cout`? Try it out and report your results.

## PRACTICE EXERCISES

**E8.1** Write a program that carries out the following tasks:
- Open a file with the name hello.txt.
- Store the message "Hello, World!" in the file.
- Close the file.
- Open the same file again.
- Read the message into a string variable and print it.

**E8.2** Write a program that reads a text file containing floating-point numbers. Print the average of the numbers in the file. Prompt the user for the file name.

**E8.3** Repeat Exercise E8.2, but allow the user to specify the file name on the command-line. If the user doesn't specify any file name, then prompt the user for the name.

**E8.4** Write a program that reads a file containing two columns of floating-point numbers. Prompt the user for the file name. Print the average of each column.

**E8.5** Write a program that reads each line in a file, reverses its characters, and writes the resulting line to another file. Suppose the user specifies input.txt and output.txt when prompted for the file names, and input.txt contains the lines
Mary had a little lamb
Its fleece was white as snow
And everywhere that Mary went
The lamb was sure to go.
After the program is finished, output.txt should contain
bmal ettli a dah yraM
wons sa etihw saw eceelf stI
tnew yraM taht erehwyere dnA
.og ot erus saw bmal ehT

**E8.6** Write a program that reads each line in a file, reverses its characters, and writes the resulting line to the same file. Use the following pseudocode:
While the end of the file has not been reached
pos1 = current get position
Read a line.
If the line was successfully read
pos2 = current get position
Set put position to pos1.
Write the reversed line.
Set get position to pos2.

**E8.7** Write a program that reads each line in a file, reverses its lines, and writes them to another file. Suppose the user specifies input.txt and output.txt when prompted for the file names, and input.txt contains the lines
Mary had a little lamb
Its fleece was white as snow
And everywhere that Mary went
The lamb was sure to go.
After the program is finished, output.txt should contain
The lamb was sure to go.
And everywhere that Mary went
Its fleece was white as snow
Mary had a little lamb

E8.8 Write a program that asks the user for a file name and displays the number of characters, words, and lines in that file. Then have the program ask for the name of the next file. When the user enters a file that doesn't exist (such as the empty string), the program should exit.

E8.9 Write a program copyfile that copies one file to another. The file names are specified on the command line. For example,
`copyfile report.txt report.sav`

E8.10 Write a program that concatenates the contents of several files into one file. For example,
`catfiles chapter1.txt chapter2.txt chapter3.txt book.txt`
makes a long file book.txt that contains the contents of the files chapter1.txt, chapter2.txt, and chapter3.txt. The target file is always the last file specified on the command line.

E8.11 Write a program that reads a file, removes any blank lines, and writes the non-blank lines back to the same file.

E8.12 Write a program that reads a file, removes any blank lines at the beginning or end of the file, and writes the remaining lines back to the same file.

## PROGRAMMING PROJECTS

P8.1 Write a program find that searches all files specified on the command line and prints out all lines containing a keyword. For example, if you call
`find Tim report.txt address.txt homework.cpp`
then the program might print
`report.txt: discussed the results of my meeting with Tim T`
`address.txt: Torrey, Tim|11801 Trenton Court|Dallas|TX`
`address.txt: Walters, Winnie|59 Timothy Circle|Detroit|MI`
`homework.cpp: Time now;`
The keyword is always the first command-line argument.

P8.2 Write a program that checks the spelling of all words in a file. It should read each word of a file and check whether it is contained in a word list. A word list is available on most UNIX systems (including Linux and Mac OS X) in the file /usr/share/dict/words. (If you don't have access to a UNIX system, you can find a copy of the file on the Internet by searching for /usr/share/dict/words.) The program should print out all words that it cannot find in the word list. Follow this pseudocode:
`Open the dictionary file.`
`Define a vector of strings called words.`
`For each word in the dictionary file`
`Append the word to the words vector.`
`Open the file to be checked.`
`For each word in that file`
`If the word is not contained in the words vector`
`Print the word.`

P8.3 Get the data for names in prior decades from the Social Security Administration. Paste the table data in files named babynames80s.txt, etc. Modify the sec01/babynames.cpp
