
```cpp
char gross[144];
cin.read(gross, 144);
```

Unlike getline() and get(), read() does not append a null character to input, so it doesn't convert input to string form. The read() method is not intended for keyboard input. Instead, it is most often used in conjunction with the ostream write() function for file input and output. The method's return type is istream &, so it can be concatenated as follows:

```cpp
char gross[144];
char score[20];
cin.read(gross, 144).read(score, 20);
```

The peek() function returns the next character from input without extracting from the input stream. That is, it lets you peek at the next character. Suppose you want to read input up to the first newline or period, whichever comes first. You can use peek() to peek at the next character in the input stream in order to judge whether to continue:

```cpp
char great_input[80];
char ch;
int i = 0;
while ((ch = cin.peek()) != '.' && ch != '\n')
    cin.get(great_input[i++]);
great_input[i] = '\0';
```

The call to cin.peek() peeks at the next input character and assigns its value to ch. Then the while loop test condition checks that ch is neither a period nor a newline. If this is the case, the loop reads the character into the array and updates the array index. When the loop terminates, the period or newline character remains in the input stream, positioned to be the first character read by the next input operation. Then the code appends a null character to the array, making it a string.

The gcount() method returns the number of characters read by the last unformatted extraction method. That means characters read by a get(), getline(), ignore(), or read() method but not by the extraction operator (>>), which formats input to fit particular data types. For example, suppose you've just used cin.get(myarray, 80) to read a line into the myarray array and you want to know how many characters were read. You could use the strlen() function to count the characters in the array, but it would be quicker to use cin.gcount() to report how many characters were just read from the input stream.

The putback() function inserts a character back in the input stream. The inserted character then becomes the first character read by the next input statement. The putback() method takes one char argument, which is the character to be inserted, and it returns type istream &, which allows the call to be concatenated with other istream methods. Using peek() is like using get() to read a character and then using putback() to place the character back in the input stream. However, putback() gives you the option of putting back a character that is different from the one just read.

Listing 17.14 uses two approaches to read and echo input up to, but not including, a # character. The first approach reads through the # character and then uses putback() to insert the character back into the input. The second approach uses peek() to look ahead before reading input.

### Listing 17.14 `peeker.cpp`

```cpp
// peeker.cpp -- some istream methods
#include <iostream>

int main()
{
    using std::cout;
    using std::cin;
    using std::endl;

// read and echo input up to a # character
    char ch;

    while(cin.get(ch))        // terminates on EOF
    {
        if (ch != '#')
            cout << ch;
        else
        {
            cin.putback(ch);    // reinsert character
            break;
        }
    }

    if (!cin.eof())
    {
        cin.get(ch);
        cout << endl << ch << " is next input character.\n";
    }
    else
    {
        cout << "End of file reached.\n";
        std::exit(0);
    }

    while(cin.peek() != '#')    // look ahead
    {
        cin.get(ch);
        cout << ch;
    }
    if (!cin.eof())
    {
        cin.get(ch);
        cout << endl << ch << " is next input character.\n";
    }
    else
        cout << "End of file reached.\n";

    return 0;
}
```

Here is a sample run of the program in Listing 17.14:

```text
I used a #3 pencil when I should have used a #2.
I used a
# is next input character.
3 pencil when I should have used a
# is next input character.
```

### Program Notes

Let’s look more closely at some of the code in Listing 17.14. The first approach uses a while loop to read input:

```cpp
while(cin.get(ch))          // terminates on EOF
{
    if (ch != '#')
        cout << ch;
    else
    {
        cin.putback(ch);  // reinsert character
        break;
    }
}
```

The expression cin.get(ch) returns false on reaching the end-of-file condition, so simulating end-of-file from the keyboard terminates the loop. If the # character shows up first, the program puts the character back in the input stream and uses a break statement to terminate the loop.

The second approach is simpler in appearance:

```cpp
while(cin.peek() != '#')    // look ahead
{
    cin.get(ch);
    cout << ch;
}
```

The program peeks at the next character. If it is not the `#` character, the program reads the next character, echoes it, and peeks at the next character. This continues until the terminating character shows up.

Now let's look, as promised, at an example—Listing 17.15—that uses `get()` to determine whether an entire line has been read. If only part of a line fits in the input array, the program discards the rest of the line.

### Listing 17.15 `truncate.cpp`

```cpp
// truncate.cpp -- using get() to truncate input line, if necessary
#include <iostream>
const int SLEN = 10;
inline void eatline() { while (std::cin.get() != '\n') continue; }
int main()
{
    using std::cin;
    using std::cout;
    using std::endl;

    char name[SLEN];
    char title[SLEN];
    cout << "Enter your name: ";
    cin.get(name,SLEN);
    if (cin.peek() != '\n')
        cout << "Sorry, we only have enough room for "
             << name << endl;

    eatline();
    cout << "Dear " << name << ", enter your title: \n";
    cin.get(title,SLEN);
    if (cin.peek() != '\n')
        cout << "We were forced to truncate your title.\n";
    eatline();
    cout << "Name: " << name
         << "\nTitle: " << title << endl;

    return 0;
}
```

Here is a sample run of the program in Listing 17.15:

```text
Enter your name: Ella Fishsniffer
Sorry, we only have enough room for Ella Fish
Dear Ella Fish, enter your title:
Executive Adjunct
We were forced to truncate your title.
Name: Ella Fish
Title: Executive
```

Note that the following code makes sense whether or not the first input statement reads the entire line:

```cpp
while (cin.get() != '\n') continue;
```

If get() reads the whole line, it still leaves the newline in place, and this code reads and discards the newline character. If get() reads just part of the line, this code reads and discards the rest of the line. If you didn't dispose of the rest of the line, the next input statement would begin reading at the beginning of the remaining input on the first input line. With this example, that would result in the program reading the string sniffer into the title array.

## File Input and Output

Most computer programs work with files. Word processors create document files. Database programs create and search files of information. Compilers read source code files and generate executable files. A file itself is a bunch of bytes stored on some device, perhaps magnetic tape, perhaps an optical disk, a floppy disk, or a hard disk. Typically, the operating system manages files, keeping track of their locations, their sizes, when they were created, and so on. Unless you're programming on the operating system level, you normally don't have to worry about those things. What you do need is a way to connect a program to a file, a way to have a program read the contents of a file, and a way to have a program create and write to files. Redirection (as discussed earlier in this chapter) can provide some file support, but it is more limited than explicit file I/O from within a program. Also redirection comes from the operating system, not from C++, so it isn't available on all systems. This book has already touched on file I/O, and this chapter explores the topic more thoroughly.

The C++ I/O class package handles file input and output much as it handles standard input and output. To write to a file, you create an ofstream object and use the ostream methods, such as the << insertion operator or write(). To read a file, you create an ifstream object and use the istream methods, such as the >> extraction operator or get(). Files require more management than the standard input and output, however. For example, you have to associate a newly opened file with a stream. You can open a file in read-only mode, write-only mode, or read-and-write mode. If you write to a file, you might want to create a new file, replace an old file, or add to an old file. Or you might want to move back and forth through a file. To help handle these tasks, C++ defines several new classes in the fstream (formerly fstream.h) header file, including the ifstream class for file input and the ofstream class for file output. C++ also defines the fstream class for simultaneous file I/O. These classes are derived from the classes in the iostream header file, so objects of these new classes are able to use the methods you've already learned.
