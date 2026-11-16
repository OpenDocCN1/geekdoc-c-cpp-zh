
- **cputs(char *str)** Writes the null-terminated string str to the current text window. It does not append a newline character.

- **cprintf(..)** Displays formatted output to the text window on the screen.

- **cscanf(..)** Reads formatted input from the text window.

- **getch()** Reads a character from console but does not echo to the screen.

- **getche()** Reads a character from console and echoes to the screen.

- **gotoxy()** Positions cursor in text window.

- **movetext()** Copies text on screen from one rectangle to another.

- **gettext()** Copies text from text-mode screen to memory.

- **puttext()** Copies text from memory to text-mode screen.

- **kbhit()** Checks for currently available keystrokes.

- **putch()** Displays the character to the current text window.

- **textbackground()** Selects a new text background color.

- **window()** Defines active text-mode window.

## CHARACTER CLASSIFICATION FUNCTIONS ( Include file is ctype.h )

- **isalnum(c)** Determine if argument is alphanumeric. Return non-zero value if true; 0 otherwise.

- **isalpha(c)** Determine if argument is alphabetic. Return non-zero value if true; 0 otherwise.

- **isascii(c)** Determine if argument is an ASCII character. Return non-zero value if true; 0 otherwise.

- **iscntrl(c)** Determine if argument is an ASCII character. Return non-zero value if true; 0 otherwise.

- **isdigit(c)** Determine if argument is a decimal digit character. Return non-zero value if true; 0 otherwise.

- **isgraph(c)** Determine if argument is a graphic ASCII character. Return non-zero value if true; 0 otherwise.

- **islower(c)** Determine if argument is lowercase. Return non-zero value if true; 0 otherwise.

- **isodigit(c)** Determine if argument is graphic ASCII character. Return non-zero value if true; 0 otherwise.

- **isprint(c)** Determine if argument is a printing ASCII character. Return non-zero value if true; 0 otherwise.

- **isspace(c)** Determine if argument is a white space character. Return non-zero value if true; 0 otherwise.

- **isupper(c)** Determine if argument is uppercase. Return non-zero value if true; 0 otherwise.

- **isxdigit(c)** Determine if argument is hexadecimal digit. Return non-zero value if true; 0 otherwise.

- **tolower(c)** Tests the character and converts to lowercase if uppercase.

- **toupper(c)** Tests the character and converts to uppercase if lowercase.

## DIRECTORY FUNCTIONS (include file is dir.h)

- **chdir(char *path)** Causes the directory specified by path to become the current working directory.

- **findfirst(char *path)** Uses the DOS system call 0x4E to begin a search of a disk directory.

- **findnext(char *path)** Finds subsequent files that match the pathname argument of findfirst.

- **getcurdir()** Gets current directory for specified drive.

- **getcwd()** Gets the current working directory.

- **mkdir(char *path)** Creates a new directory from the given path.

- **rmdir(char *path)** Deletes the directory whose path is given by path.

- **searchpath(char *p)** Searches the DOS path (p) for a file.

## DISK OPERATING SYSTEM FUNCTIONS (include file is dos.h)

- **absread()** Uses DOS interrupt 0x25 to read specific disk sectors.

- **abswrite()** Uses DOS interrupt 0x26 to write specific disk sectors.

- **allocmem()** Uses the DOS system call 0x48 to allocate a block of free memory and return the segment address of the allocated block.

- **delay()** Suspends execution of a program for an interval in milliseconds.

- **disable()** Used to disable interrupts.

- **dostounix()** Converts date and time to UNIX time.

- **enable()** Used to enable interrupts.

- **freemem()** Frees a previously allocated DOS memory block.

- **geninterrupt()** Macro that generates a software interrupt.

- **getdate()** Gets DOS system date.

- **gettime()** Gets DOS system time.

- **inport()** Reads a word from a hardware port.

- **inportb()** Reads a byte from a hardware port.

- **int86()** Used to execute an 8086 software interrupt.

- **intdos()** Used to execute DOS interrupt 0x21 to invoke a specified DOS function.

- **intdosx()** Used to execute DOS interrupt 0x21 to invoke a specified DOS function.

- **intr()** An alternate interface for executing software interrupts, that generates an 8086 software interrupt.

- **keep()** Exits the current program and remains resident.

- **nosound()** Turns the PC speaker off.

- **outport()** Sends a word to a hardware port.

- **outportb()** Sends a byte to a hardware port.

- **setdate()** Sets DOS system date.

- **settime()** Sets DOS system time.

- **sleep()** Suspends execution for an interval in milliseconds.

- **sound()** Turns the PC speaker on at the specified frequency.

- **unixtodos()** Converts date and time from UNIX to DOS format.

## INPUT / OUTPUT FUNCTIONS ( include file is io.h )

- **access()** Determines the accessibility of a file.

- **chmod()** Sets file access permissions (read, write & execute).

- **chsize()** Changes the size of the file.

- **close()** Closes a file previously opened by open().

- **creat()** Creates a new file or overwrite an existing one.

- **creatnew()** Creates and opens a new file for reading & writing in binary mode.

- **eof()** Checks for end-of-file.

- **filelength()** Gets file size in bytes.

- **lock()** Sets or resets file-sharing locks.

- **mktemp()** Makes a unique file name.

- **open()** Opens a file.

- **read()** Uses DOS function 0x3F (read system call) to read bytes from a file into a buffer.

- **remove()** Macro that removes a file.

- **rename()** Changes the name of a file from oldname to newname.

- **tell()** Gets current position of file pointer.

- **write()** Uses DOS function 0x40 to write bytes from a buffer to a file.

## ARITHMETIC FUNCTIONS ( Include file is math.h )

- **cos(d)** Returns the cosine value of double d.

- **cosh(d)** Returns the hyperbolic cosine value of double d.

- **ceil(d)** Returns a value rounded up to the next higher integer.

- **acos(d)** Returns the arc cosine of d.

- **asin(d)** Raises the exponential to the power d.

- **exp(d)** Returns the value of power d.

- **fabs(d)** Returns the absolute value of d.

- **floor(d)** Returns the value rounded down to the next lower integer.

- **fmod(d, d2)** Returns the remainder of d / d2.

- **hypot(d)** Returns the hypotenuse of right triangle.

- **log(d)** Returns the natural logarithm of d.

- **log10(d)** Returns the natural logarithm of d.

- **modf(d)** Returns the argument into integer and fractional parts.

- **pow(d, d2)** Returns d, raised to the d2 power.

- **sin(d)** Returns the sine of d.

- **sinh(d)** Returns the hyperbolic sine of d.

- **sqrt(d)** Returns the square root of d.

- **tan(d)** Returns the tangent of d.

- **tanh(d)** Returns the hyperbolic tangent of d.

## MEMORY FUNCTIONS (include file is mem.h)

- **memcpy()** Copies a block of n bytes from source to destination.

- **memchr()** Searches for a character in a string of n bytes.

- **memcmp()** Compares the first n bytes of strings s1 and s2.

- **memicmp()** Compares the first n bytes of strings s1 and s2, ignoring case.

- **memmove()** Moves a block of n bytes from source to destination.

- **movmem()** Moves a block of length bytes from source to destination.

- **setmem()** Sets a block of length bytes in memory.

## PROCESS FUNCTIONS (include file is process.h)

- **abort()** Abnormally terminates a process.

- **exec()** Enable your program to load and run other files (child processes).

- **exit()** Terminates the program.

- **getpid()** Gets the process ID of the program.

- **spawnl()** Enable your programs to run other files (child processes) and returns control to your program when the child processes finish.

- **system()** Invokes the DOS command interpreter file from inside an executing C program to execute a DOS command.

## JUMP FUNCTIONS (include file is setjmp.h)

- **longjmp()** Performs a nonlocal goto.

- **setjmp()** Sets up for a nonlocal goto.

## SIGNAL RECEIVING / SENDING FUNCTIONS (include file is signal.h)

- **raise()** Sends a software signal to the executing program.

- **signal()** Specifies signal-handling actions.

## DATA CONVERSION FUNCTIONS ( Include file is stdlib.h )

- **atof(s)** Converts string to float.

- **atoi(s)** Converts string to int.

- **atol(s)** Converts string to long.

- **atos(s)** Converts string to long.

- **abs(i)** Returns the absolute value of an integer.

- **ecvt(d)** Converts double to string.

- **fcvt(d)** Converts double to string.

- **gcvt(d)** Converts double to string.

- **itoa(i)** Converts int to string.

- **strtod(s)** Converts long to string.

- **strtol(s)** Converts string to double.

- **strtoul(s)** Converts string to an unsigned long integer.

- **ultoa(l)** Converts unsigned long integer to string.
