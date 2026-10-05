
# Contents

## Chapter 1 C++ Basics 1
### 1.1 INTRODUCTION TO C++ 2
Origins of the C++ Language 2
C++ and Object-Oriented Programming 3
The Character of C++ 3
C++ Terminology 4
A Sample C++ Program 4

### 1.2 VARIABLES, EXPRESSIONS, AND ASSIGNMENT STATEMENTS 6
Identifiers 7
Variables 8
Assignment Statements 10
Introduction to the string class 12
PITFALL: Uninitialized Variables 12
TIP: Use Meaningful Names 13
More Assignment Statements 14
Assignment Compatibility 15
Literals 16
Escape Sequences 17
Naming Constants 17
Arithmetic Operators and Expressions 19
Integer and Floating-Point Division 21
PITFALL: Division with Whole Numbers 22
Type Casting 23
Increment and Decrement Operators 25
PITFALL: Order of Evaluation 27

### 1.3 CONSOLE INPUT/OUTPUT 28
Output Using cout 28
New Lines in Output 29
TIP: End Each Program with \n or endl 29
Formatting for Numbers with a Decimal Point 32
Output with cerr 32
Input Using cin 32
TIP: Line Breaks in I/O 35

### 1.4 PROGRAM STYLE 36
Comments 36

### 1.5 LIBRARIES AND NAMESPACES 37
Libraries and include Directives 37
Namespaces 37
PITFALL: Problems with Library Names 38

Chapter Summary 39
Answers to Self-Test Exercises 40
Programming Projects 42

## Chapter 2 Flow of Control 45
### 2.1 BOOLEAN EXPRESSIONS 45
Building Boolean Expressions 46
PITFALL: Strings of Inequalities 47
Evaluating Boolean Expressions 48
Precedence Rules 50
PITFALL: Integer Values Can Be Used as Boolean Values 53

### 2.2 BRANCHING MECHANISMS 56
if-else Statements 56
Compound Statements 58
PITFALL: Using = in Place of == 59
Omitting the else 61
Nested Statements 61
Multiway if-else Statement 61
The switch Statement 62
PITFALL: Forgetting a break in a switch Statement 65
TIP: Use switch Statements for Menus 66
Enumeration Types 66
The Conditional Operator 66

### 2.3 LOOPS 67
The while and do-while Statements 68
Increment and Decrement Operators Revisited 71
The Comma Operator 72
The for Statement 74
TIP: Repeat-N-Times Loops 76
PITFALL: Extra Semicolon in a for Statement 77
PITFALL: Infinite Loops 77
The break and continue Statements 88
Nested Loops 83

### 2.4 INTRODUCTION TO FILE INPUT 83
Reading From a Text File Using istream 84

Chapter Summary 87
Answers to Self-Test Exercises 87
Programming Projects 93

## Chapter 3 Function Basics 99
### 3.1 PREDEFINED FUNCTIONS 100
Predefined Functions That Return a Value 100
Predefined void Functions 105
A Random Number Generator 107

### 3.2 PROGRAMMER-DEFINED FUNCTIONS 111
Defining Functions That Return a Value 112
Alternate Form for Function Declarations 114
PITFALL: Arguments in the Wrong Order 115
PITFALL: Use of Terms Parameter and Argument 115
Functions Calling Functions 115
EXAMPLE: A Rounding Function 115
Functions That Return a Boolean Value 119
Defining void Functions 119
return Statements in void Functions 121
Preconditions and Postconditions 121
main Is a Function 123
Recursive Functions 123

### 3.3 SCOPE RULES 125
Local Variables 125
Procedural Abstraction 127
Global Constants and Global Variables 128
Blocks 131
Nested Scopes 132
TIP: Use Function Calls in Branching and Loop Statements 132
Variables Declared in a for Loop 133

Chapter Summary 134
Answers to Self-Test Exercises 132
Programming Projects 138

## Chapter 4 Parameters and Overloading 145
### 4.1 PARAMETERS 146
Call-by-Value Parameters 146
A First Look at Call-by-Reference Parameters 148
Call-by-Reference Mechanism in Detail 151
Constant Reference Parameters 153
EXAMPLE: swapValues Function 153
TIP: Think of Actions, Not Code 154
Mixed Parameter Lists 155
TIP: What Kind of Parameter to Use 156
PITFALL: Inadvertent Local Variables 158
TIP: Choosing Formal Parameter Names 159
EXAMPLE: Buying Pizza 160

### 4.2 OVERLOADING AND DEFAULT ARGUMENTS 163
Introduction to Overloading 163
PITFALL: Automatic Conversion and Overloading 166
Rules for Resolving Overloading 167
EXAMPLE: Revised Pizza-Buying Program 169
Default Arguments 171

Chapter Summary 177
Answers to Self-Test Exercises 179
Programming Projects 179

## Chapter 5 Arrays 185
### 5.1 INTRODUCTION TO ARRAYS 186
Declaring and Referencing Arrays 186
TIP: Use for Loops with Arrays 189
PITFALL: Array Indexes Always Start with Zero 189
TIP: Use a Defined Constant for the Size of an Array 189
Arrays in Memory 190
PITFALL: Array Index out of Range 192
Initializing Arrays 192

### 5.2 ARRAYS IN FUNCTIONS 195
Indexed Variables as Function Arguments 195
Entire Arrays as Function Arguments 196
The const Parameter Modifier 200
PITFALL: Inconsistent Use of const Parameters 201
Functions That Return an Array 202
EXAMPLE: Production Graph 202

### 5.3 PROGRAMMING WITH ARRAYS 207
Partially Filled Arrays 207
TIP: Do Not Skimp on Formal Parameters 208
EXAMPLE: Searching for an Array 211
EXAMPLE: Sorting an Array 213

### 5.4 MULTIDENSIONAL ARRAYS 218
Multidimensional Array Basics 218
Multidimensional Array Parameters 219
EXAMPLE: Two-Dimensional Grading Program 220

Chapter Summary 225
Answers to Self-Test Exercises 226
Programming Projects 230

## Chapter 6 Structures and Classes 239
### 6.1 STRUCTURES 240
Structure Types 242
PITFALL: Forgetting a Semicolon in a Structure Definition 246
Structures as Function Arguments 246
TIP: Use Hierarchical Structures 247
Initializing Structures 249

### 6.2 CLASSES 252
Defining Classes and Member Functions 258
Encapsulation 258
Public and Private Members 259
Accessor and Mutator Functions 262
TIP: Separator Interface and Implementation 264
TIP: A Class Has Access 265
Structures vs Classes 266
Structures vs Classes 268

Chapter Summary 268
Answers to Self-Test Exercises 269
Programming Projects 271

## Chapter 7 Constructors and Other Tools 275
### 7.1 CONSTRUCTORS 276
Constructors 276
PITFALL: Constructors with Arguments 281
Explicit Constructor 282
TIP: A Constructor Can Return Object 283
Member Variables 285

### 7.2 MORE TOOLS 295
The const Parameter Modifier 295
PITFALL: Inconsistent Use of const Parameters 297
Inline Functions 301
Static Members 303

### 7.3 THE STANDARD CLASS string 307
Introduction to the Standard Class string 307
I/O with the Class string 396
TIP: More Versions of getline 399
PITFALL: Mixing cin >> variable; and getline 399
String Processing with the Class string 401

Chapter Summary 313
Answers to Self-Test Exercises 313
Programming Projects 31

## Chapter 8 Operator Overloading, Friends, and References 323
### 8.1 BASIC OPERATOR OVERLOADING 323
Operator Overloading 323
PITFALL: Overloading 328
TIP: A Constructor Can Return Object 329
Unary Operators 332
Member Functions 335

### 8.2 FRIEND FUNCTIONS AND AUTOMATIC CONVERSION 336
Friend Functions 336
Automatic Type Conversion 337
Friend Functions 338
Friend Classes 341
PITFALL: Compilers without Friends 342

### 8.3 REFERENCES AND MORE OVERLOADED OPERATORS 343
References 344
TIP: Returning Member Variables of a Class 345
Overloading >> and << 346
TIP: What Mode of Returned Value to Use 352
Assignment Operator 355
Increment and Decrement Operators 355
Array Operator [] 358
Overloading Based on L-Value versus R-Value 360

Chapter Summary 360
Answers to Self-Test Exercises 361
Programming Projects 363

## Chapter 9 Strings 367
### 9.1 AN ARRAY TYPE FOR STRINGS 368
C-Strings 368
C-String Values and C-String Variables 369
PITFALL: Using and = = with C-strings 372
Other Functions in <cstring> 374
EXAMPLE: Command-Line Arguments 374
C-String Input and Output 379

### 9.2 CHARACTER MANIPULATION TOOLS 381
Character I/O 381
The Member Functions get and put 382
EXAMPLE: Checking Input Using a Newline Function 384
PITFALL: Unexpected '\' in Input 386
The putback, peek, and ignore Member Functions 387
Character-Manipulating Functions 389
PITFALL: toupper and colower Return int Values 391

### 9.3 THE STANDARD CLASS string 393
Introduction to the Standard Class string 393
I/O with the Class string 396
TIP: More Versions of getline 399
PITFALL: Mixing cin >> variable; and getline 399
String Processing with the Class string 401
EXAMPLE: Palindrome Testing 404
Converting between string Objects and C-Strings 408

Chapter Summary 409
Answers to Self-Test Exercises 409
Programming Projects 413
