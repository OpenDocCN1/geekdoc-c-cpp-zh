# 1110 Chapter 17 Input, Output, and Files

char gross[144];
cinc.read(gross, 144);

Unlike getline() and get(), read() does not append a null character to input, so it doesn't convert input to string form. The read() method is not intended for keyboard input. It is most often used in conjunction with the ostream write() function for file input and output. The method's return type is istream&, so it can be concatenated as follows:

```
char gross[144];nchar score[20];ncinc.read(gross, 144).read(score, 20);
```

The peek() function returns the next character from input without extracting from the input stream. It then lets you peek at the next character. Suppose you want to read input up to the first newline, whichever comes first. You can use peek() to peek at the next character in the input stream in order to judge whether to continue:

```
char great_input[80];nchar ch;
 i = 0;
while ((ch = cin.peek()) != '.' && ch != '\n')
cin.get(great_input[i++]);
great_input[i] = '\0';
```

The call to peek() views the next character and assigns its value to ch. Then the loop test checks that ch is neither a period nor a newline. If this is the case, the loop reads the character into the array and updates the index. When the loop terminates, the period or newline character remains in the input stream, positioned to the first character read by the next input operation. Then the code appends a null character to the array, making it string.

The count() method returns the number of characters read by the last unformatted extraction method. That means characters read by a get(), getline(), ignore(), or read() method not by the extraction operator (>), which formats input to fit particular types. For example, suppose you've used cin.get(my, 80) to read a line into the array and want to know how many characters were read. You could use the strlen() function to count the characters in the array, but it would be quicker to use cin.count() to report how many characters were read from the input stream

The putback() function inserts a character back into the input string. The inserted character then becomes the first character read by the next input statement. The putback() method takes one argument, which is the character to be inserted, and returns type istream&, which allows it to be concatenated with other istream methods. Using peek() is like using get() to read a character and then using putback() to place the character back in the input stream. However, putback() gives you the option of putting back a character that is different from the one just read.