
## The ASCII Character Set

Only the printable characters are shown. Character number 32 is the blank.

| 32 | 56 | 8 | 80 | P | 104 | h |
|---|---|---|---|---|---|---|
| 33 | ! | 57 | 9 | 81 | Q | 105 | i |
| 34 | " | 58 | : | 82 | R | 106 | j |
| 35 | # | 59 | ; | 83 | S | 107 | k |
| 36 | $ | 60 | < | 84 | T | 108 | l |
| 37 | % | 61 | = | 85 | U | 109 | m |
| 38 | & | 62 | > | 86 | V | 110 | n |
| 39 | ' | 63 | ? | 87 | W | 111 | o |
| 40 | ( | 64 | @ | 88 | X | 112 | p |
| 41 | ) | 65 | A | 89 | Y | 113 | q |
| 42 | * | 66 | B | 90 | Z | 114 | r |
| 43 | + | 67 | C | 91 | [ | 115 | s |
| 44 | , | 68 | D | 92 | \ | 116 | t |
| 45 | - | 69 | E | 93 | ] | 117 | u |
| 46 | . | 70 | F | 94 | ^ | 118 | v |
| 47 | / | 71 | G | 95 | _ | 119 | w |
| 48 | 0 | 72 | H | 96 | ` | 120 | x |
| 49 | 1 | 73 | I | 97 | a | 121 | y |
| 50 | 2 | 74 | J | 98 | b | 122 | z |
| 51 | 3 | 75 | K | 99 | c | 123 | { |
| 52 | 4 | 76 | L | 100 | d | 124 | | |
| 53 | 5 | 77 | M | 101 | e | 125 | } |
| 54 | 6 | 78 | N | 102 | f | 126 | ~ |
| 55 | 7 | 79 | O | 103 | g |  |  |

## APPENDIX 4
Some Library Functions

The following lists are organized according to what the function is used for, rather than what library it is in. The function declaration gives the number and types of arguments as well as the type of the value returned. In most cases, the function declarations give only the type of the parameter and do not give a parameter name. (See the section "Alternate Form for Function Declarations" in Chapter 4 for an explanation of this kind of function declaration.)

### Arithmetic Functions

| Function Declaration | Description | Header File |
|---|---|---|
| `int abs(int);` | Absolute value | cstdlib |
| `long labs(long);` | Absolute value | cstdlib |
| `double fabs(double);` | Absolute value | cmath |
| `double sqrt(double);` | Square root | cmath |
| `double pow(double,double);` | Returns the first argument raised to the power of the second argument. | cmath |
| `double exp(double);` | Returns e (base of the natural logarithm) to the power of its argument. | cmath |
| `double log(double);` | Natural logarithm (ln) | cmath |
| `double log10(double);` | Base 10 logarithm | cmath |
| `double ceil(double);` | Returns the smallest integer that is greater than or equal to its argument. | cmath |
| `double floor(double);` | Returns the largest integer that is less than or equal to its argument. | cmath |

### Input and Output Member Functions

| Form of a Function Call | Description | Header File |
|---|---|---|
| Stream_Var.open (External_File_Name); | Connects the file with the External_File_Name to the stream named by the Stream_Var. The External_File_Name is a string value. | fstream |
| Stream_Var.fail(); | Returns true if the previous operation (such as open) on the stream Stream_Var has failed. | fstream or iostream |
| Stream_Var.close(); | Disconnects the stream Stream_Var from the file it is connected to. | fstream |
| Stream_Var.bad(); | Returns true if the stream Stream_Var is corrupted. | fstream or iostream |
| Stream_Var.eof(); | Returns true if the program has attempted to read beyond the last character in the file connected to the input stream Stream_Var. Otherwise, it returns false. | fstream or iostream |
| Stream_Var.get (Char_Variable); | Reads one character from the input stream Stream_Var and sets the Char_Variable equal to this character. Does not skip over whitespace. | fstream or iostream |
| Stream_Var.getline (String_Var, Max_Characters +1); | One line of input from the stream Stream_Var is read, and the resulting string is placed in String_Var. If the line is more than Max_Characters long, only the first Max_Characters are read. The declared size of the String_Var should be Max_Characters +1 or larger. | fstream or iostream |
| Stream_Var.peek(); | Reads one character from the input stream Stream_Var and returns that character. But the character read is not removed from the input stream; the next read will read the same character. | fstream or iostream |
| Stream_Var.put (Char_Exp); | Writes the value of the Char_Exp to the output stream Stream_Var. | fstream or iostream |
| Stream_Var.putback (Char_Exp); | Places the value of Char_Exp in the input stream Stream_Var so that that value is the next input value read from the stream. The file connected to the stream is not changed. | fstream or iostream |
| Stream_Var.precision (Int_Exp); | Specifies the number of digits output after the decimal point for floating-point values sent to the output stream Stream_Var. | fstream or iostream |
| Stream_Var.width (Int_Exp); | Sets the field width for the next value output to the stream Stream_Var. | fstream or iostream |
| Stream_Var.setf(Flag); | Sets flags for formatting output to the stream Stream_Var. See Display 6.5 for the list of possible flags. | fstream or iostream |
| Stream_Var.unsetf(Flag); | Unsets flags for formatting output to the stream Stream_Var. See Display 6.5 for the list of possible flags. | fstream or iostream |

### String Functions

| Function Declaration | Description | Header File |
|---|---|---|
| `int atoi(const char[]);` | Converts a string of characters to an integer. | `cstdlib` |
| `int stoi(const string)` | Converts a STL string object to an integer. C++11 and higher. | `string` |
| `long atol(const char[]);` | Converts a string of characters to a *long* integer. | `cstdlib` |
| `long stol(const string)` | Converts a STL string object to a long. C++11 and higher. | `string` |
| `double atof(const char a[]);` | Converts a string of characters to a *double*. | `cstdlib`¹ |
| `strcat(String_Variable, String_Expression);` | Appends the value of the *String_Expression* to the end of the string in the *String_Variable*. | `cstring` |
| `strcmp(String_Exp1, String_Exp2)` | Returns *true* if the values of the two string expressions are different; otherwise, returns *false*.² | `cstring` |
| `strcpy(String_Variable, String_Expression);` | Changes the value of the *String_Variable* to the value of the *String_Expression*. | `cstring` |
| `strlen(String_Expression)` | Returns the length of the *String_Expression*. | `cstring` |
| `strncat(String_Variable, String_Expression, Limit);` | Same as strcat except that at most *Limit* characters are appended. | `cstring` |
| `strncmp(String_Exp1, String_Exp2, Limit)` | Same as strcmp except that at most *Limit* characters are compared. | `cstring` |
| `strncpy(String_Variable, String_Expression, Limit);` | Same as strcpy except that at most *Limit* characters are copied. | `cstring` |
| `strstr(String_Expression, Pattern)` | Returns a pointer to the first occurrence of the string *Pattern* in *String_Expression*. Returns the NULL pointer if the *Pattern* is not found. | `cstring` |
| `strchr(String_Expression, Character)` | Returns a pointer to the first occurrence of the *Character* in *String_Expression*. Returns the NULL pointer if *Character* is not found. | `cstring` |
| `strrchr(String_Expression, Character)` | Returns a pointer to the last occurrence of the *Character* in *String_Expression*. Returns the NULL pointer if *Character* is not found. | `cstring` |

¹ Some implementations place it in cmath.

² Returns an integer that is less than zero, zero, or greater than zero according to whether String_Exp1 is less than, equal to, or greater than String_Exp2, respectively. The ordering is lexicographic ordering.

### Random Number Generator

| Function Declaration | Description | Header File |
|---|---|---|
| `int random(int);` | The call random(n) returns a pseudorandom integer greater than or equal to 0 and less than or equal to n−1. (Not available in all implementations. If not available, then you must use rand.) | `cstdlib` |
| `int rand();` | The call rand() returns a pseudorandom integer greater than or equal to 0 and less than or equal to RAND_MAX. RAND_MAX is a predefined integer constant that is defined in cstdlib. The value of RAND_MAX is implementation dependent but will be at least 32767. | `cstdlib` |
| `void srand(unsigned int);`<br>`void srandom(unsigned int);`<br><br>(The type `unsigned int` is an integer type that only allows nonnegative values. You can think of the argument type as `int` with the restriction that it must be nonnegative.) | Reinitializes the random number generator. The argument is the seed. Calling srand multiple times with the same argument will cause rand or random (whichever you use) to produce the same sequence of pseudorandom numbers. If rand or random is called without any previous call to srand, the sequence of numbers produced is the same as if there had been a call to srand with an argument of 1. | `cstdlib` |
