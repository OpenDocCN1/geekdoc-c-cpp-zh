| Member function | Description | Examples |
|---|---|---|
|  |  | In the following code snippet, a `filename` object of `std::string` type is created, containing a digit number of digit characters:

```cpp
int digit[3];  // 333.txt, 444.txt, ...
// ...
// Make a file containing digit digits
assert( digit >= 0 && digit < 9 );
// repeat char
string fileName( digit, '0' + digit ); // ASCII codes '0'

// Open the output file
ofstream outfile( fileName + ".txt" );

outfile << filePath << name << endl;
outFile << " lower capital letters" << endl;
```

For this purpose, a string constructor is called with the number of repeated values and the value of the character to be repeated. Adding a value of digit to the literal `'0'` is a simple way of computing the ASCII code corresponding to digit. The `assert` function verifies a condition in a debug version of the code. |

Color functions are separate from `std::string`. An analogous set is available in `std::wstring` for international character sets.