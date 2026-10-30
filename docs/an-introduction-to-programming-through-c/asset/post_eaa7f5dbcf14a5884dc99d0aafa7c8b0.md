
## An Introduction to Programming through C++

Abhiram Ranade

Do not distribute

©Abhiram Ranade, 2013

- 2.6 The arithmetic unit — 40
- 2.7 Input-Output Devices — 40
  - 2.7.1 Display — 41
  - 2.7.2 Disks — 41
  - 2.7.3 Remarks — 41
- 2.8 The Control Unit — 42
  - 2.8.1 Control Flow — 44
- 2.9 High level programming languages — 44
- 2.10 Concluding Remarks — 44
- 2.11 Exercises — 45

## 3 Numbers — 46

- 3.1 Variables and data types — 46
  - 3.1.1 Identifiers — 49
  - 3.1.2 Literals and variable initialization — 49
  - 3.1.3 The `const` keyword — 50
  - 3.1.4 Reading data into a variable — 51
  - 3.1.5 Printing — 52
  - 3.1.6 Exact representational parameters — 52
- 3.2 Arithmetic and assignment — 53
  - 3.2.1 Integer division and the modulo operator `%` — 54
  - 3.2.2 Subtleties — 55
  - 3.2.3 Overflow and arithmetic errors — 56
  - 3.2.4 Infinity and not a number — 57
  - 3.2.5 Explicit type conversion — 57
  - 3.2.6 Assignment expression — 57
- 3.3 Examples — 58
- 3.4 Assignment with repeat — 59
  - 3.4.1 Programming Idioms — 60
  - 3.4.2 Combining sequence generation and accumulation — 62
- 3.5 Some operators inspired by the idiom — 62
  - 3.5.1 Increment and decrement operators — 63
  - 3.5.2 Compound assignment operators — 63
- 3.6 Blocks and variable definitions — 64
  - 3.6.1 Block — 64
  - 3.6.2 General principle 1 — 65
  - 3.6.3 General principle 2 — 65
- 3.7 Concluding remarks — 67
- 3.8 Exercises — 67

## 4 A program design example — 71

- 4.1 Specification — 71
  - 4.1.1 Examples — 72
- 4.2 Program design — 72
  - 4.2.1 Testing — 75
  - 4.2.2 Correctness Proof — 75
  - 4.2.3 Invariants — 76
- 4.3 Debugging — 76
- 4.4 Comments in the code — 77
- 4.5 Concluding remarks — 77
  - 4.5.1 A note on programming exercises — 78
- 4.6 Exercises — 78

## 5 Simplecpp graphics

- 5.1 Overview — 80
  - 5.1.1 y axis goes downward! — 81
- 5.2 Multiple Turtles — 81
- 5.3 Other shapes besides turtles — 82
  - 5.3.1 Circles — 82
  - 5.3.2 Rectangles — 82
  - 5.3.3 Lines — 82
  - 5.3.4 Text — 83
- 5.4 Commands allowed on shapes — 83
  - 5.4.1 Rotation in radians — 84
  - 5.4.2 Tracking a shape — 84
  - 5.4.3 Imprinting on the canvas — 84
  - 5.4.4 Resetting a shape — 85
- 5.5 Clicking on the canvas — 85
- 5.6 Projectile Motion — 86
- 5.7 Best fit straight line — 87
- 5.8 Concluding Remarks — 88
- 5.9 Exercises — 88

## 6 Conditional Execution

- 6.1 The if statement — 91
- 6.2 Blocks — 95
- 6.3 Other forms of the if statement — 95
- 6.4 A different turtle controller — 98
  - 6.4.1 “Buttons” on the canvas — 99
- 6.5 The switch statement — 100
- 6.6 Conditional Expressions — 102
- 6.7 Logical Data — 102
  - 6.7.1 Reasoning about logical data — 103
  - 6.7.2 Determining whether a number is prime — 104
- 6.8 Remarks — 106
- 6.9 Exercises — 107

- 9.6 Some difficulties — 151
- 9.7 Call by reference — 152
  - 9.7.1 Remarks — 154
  - 9.7.2 Reference variables — 154
- 9.8 Pointers — 154
  - 9.8.1 “Address of” operator `&` — 155
  - 9.8.2 Pointer variables — 155
  - 9.8.3 Dereferencing operator `*` — 156
  - 9.8.4 Use in functions — 157
  - 9.8.5 Reference vs. Pointers — 158
- 9.9 Returning references and pointers — 159
- 9.10 Default values of parameters — 160
- 9.11 Function overloading — 161
- 9.12 Function templates — 162

## 10 Recursive Functions — 164

- 10.1 Euclid’s algorithm for GCD — 165
  - 10.1.1 Execution of recursive gcd — 166
  - 10.1.2 Interpretation of recursive programs — 167
  - 10.1.3 Correctness of recursive programs — 167
- 10.2 Recursive pictures — 168
  - 10.2.1 Trees without using a turtle — 171
  - 10.2.2 Hilbert space filling curve — 172
- 10.3 Virahanka numbers — 173
  - 10.3.1 Using a loop — 175
  - 10.3.2 Historical Remarks — 177
- 10.4 The game of Nim — 177
  - 10.4.1 Remarks — 180
- 10.5 Concluding remarks — 180

## 11 Program organization and functions — 185

- 11.1 The main program is a function! — 186
- 11.2 Organizing functions into files — 186
  - 11.2.1 Function Declaration or Prototype — 186
  - 11.2.2 Splitting a program into multiple files — 187
  - 11.2.3 Separate compilation and object modules — 187
  - 11.2.4 Header files — 189
  - 11.2.5 Header guards — 190
  - 11.2.6 Packaging software — 190
  - 11.2.7 Forward declaration — 191
  - 11.2.8 Function templates and header files — 191
- 11.3 Namespaces — 191
  - 11.3.1 Definition — 192
  - 11.3.2 The using declaration and directive — 193
  - 11.3.3 The global namespace — 193
  - 11.3.4 Unnamed namespaces — 194
  - 11.3.5 Namespaces and header files — 194
- 11.4 Global variables — 194
- 11.5 Two important namespaces — 196
- 11.6 C++ without simplecpp — 197
- 11.7 Function Pointers — 197
  - 11.7.1 Some simplifications — 200
- 11.8 Concluding remarks — 200
  - 11.8.1 Function size and readability — 200
- 11.9 Exercises — 201

## 12 Practice of programming: some tips and tools — 202

- 12.1 Clarity of specification — 203
- 12.2 Input-output examples and testing — 204
- 12.3 Input/output redirection — 206
- 12.4 Algorithm design — 206
  - 12.4.1 Mentally execute the program — 208
  - 12.4.2 Test cases for code coverage — 208
- 12.5 Assertions — 208
  - 12.5.1 Disabling assertions — 210
- 12.6 Debugging — 210
  - 12.6.1 Debuggers and IDEs — 210
  - 12.6.2 End of file and data input errors — 211
  - 12.6.3 Aside: Input-Output expressions — 211
- 12.7 Random numbers — 212
  - 12.7.1 The randuv function in simplecpp — 213
- 12.8 Concluding remarks — 213
- 12.9 Exercises — 214

## 13 Arrays — 215

- 13.1 Array: Collection of variables — 215
  - 13.1.1 Array element operations — 216
  - 13.1.2 Acceptable range for the index — 217
  - 13.1.3 Initializing arrays — 217
- 13.2 Examples of use — 218
  - 13.2.1 Notation for subarrays — 218
  - 13.2.2 A marks display program — 218
  - 13.2.3 Who got the highest? — 220
  - 13.2.4 General roll numbers — 220
  - 13.2.5 Histogram — 221
  - 13.2.6 A taxi dispatch program — 223
  - 13.2.7 A geometric problem — 226
- 13.3 The inside story — 227
  - 13.3.1 Out of range array indices — 228
  - 13.3.2 The array name by itself — 228
