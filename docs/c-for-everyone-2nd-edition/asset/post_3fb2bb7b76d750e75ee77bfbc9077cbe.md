
**delete operator** The operator that recycles memory to the heap.

**Derived class** A class that modifies a base class by adding data members, adding member functions, or redefining member functions.

**Directory** A structure on a disk that can hold files or other directories; also called a folder.

**Dot notation** The notation *object.function(parameters)* used to invoke a member function on an object.

**Element** A storage location in an array.

**Encapsulation** The hiding of implementation details.

**Escape character** A character in text that is not taken literally but has a special meaning when combined with the character or characters that follow it. The \\ character is an escape character in C++ strings.

**Exception** A condition that prevents a program from continuing normally.

**Executable file** The file that contains a program’s machine instructions.

**Explicit parameter** A parameter of a member function other than the object on which the function is invoked.

**Expression** A syntactical construct that is made up of constants, variables, and/or function calls, and the operators combining them.

**Extension** The last part of a file name, which specifies the file type. For example, the extension .cpp denotes a C++ file.

**Failed stream state** The state of a stream after an invalid operation has been attempted, such as reading a number when the next stream position yielded a non-digit, or reading after the end of file was reached.

**File** A sequence of bytes that is stored on disk.

**File pointer** The position within a file of the next byte to be read or written. It can be moved so as to access any byte in the file.

**Floating-point number** A number with a fractional part.

**Folder** Directory.

**Function** A sequence of statements that can be invoked multiple times, with different values for its parameter variables.

**Global variable** A variable whose scope is not restricted to a single function.

**Header file** A file that informs the compiler of features that are available in another module or library.

**Heap** A reservoir of storage from which memory can be allocated when a program runs.

**IDE (Integrated Development Environment)** A programming environment that includes an editor, compiler, and debugger.

**Implicit parameter** The object on which a member function is called. For example, in the call x.f(y), the object x is the implicit parameter of f.

**#include directive** An instruction to the preprocessor to include a header file.

**Index** The position of an element in an array.

**Inheritance** The “is-a” relationship between a general base class and a specialized derived class.

**Initialization** Setting a variable to a well-defined value when it is created.

**Integer** A number without a fractional part.

**Integer division** Taking the quotient of two integers and discarding the remainder. In C++, the / symbol denotes integer division if both arguments are integers. For example, 11 / 4 is 2, not 2.75.

**Interface** The set of functions that can be applied to objects of a given type.

**Lexicographic ordering** Ordering strings in the same order as in a dictionary, by skipping all matching characters and comparing the first nonmatching characters of both strings. For example, “orbit” comes before “orchid” in the lexicographic ordering. Note that in C++, unlike a dictionary, the ordering is case-sensitive: Z comes before a.

**Library** A set of precompiled functions that can be included in programs.

**Linker** The program that combines object and library files into an executable file.

**Local variable** A variable whose scope is a single block.

**Logic error** An error in a syntactically correct program that causes it to act differently from its specification.

**Logical operator** An operator that can be applied to Boolean values. C++ has three logical operators: &&, ||, and !.

**Loop** A sequence of instructions that is executed repeatedly.

**Loop and a half** A loop whose termination decision is neither at the beginning nor at the end.

**Machine code** Instructions that can be executed directly by the CPU.

**Magic number** A number that appears in a program without explanation.

**main function** The function that is called first when a program executes.

**Member function** A function that is defined by a class and operates on objects of that class.

**Memory** The circuitry that stores code and data in a computer.

**Syntax error** An instruction that does not follow the programming language rules and is rejected by the compiler.

**Tab character** The '\t' character, which advances the next character on the line to the next one of a set of fixed screen positions known as tab stops.

**Test coverage** The instructions of a program that are executed when a set of test cases are run.

**Text file** A file in which values are stored in their text representation.

**Trace message** A message that is printed during a program run for debugging purposes.

**Type** A named set of values and the operations that can be carried out with them.

**Unary operator** An operator with one argument.

**Unicode** A standard code that assigns values consisting of two bytes to characters used in scripts around the world.

**Uninitialized variable** A variable that has not been set to a particular value. It is filled with whatever “random” bytes happen to be present in the memory location that the variable occupies.

**Unit test** A test of a function by itself, isolated from the remainder of the program.

**Value parameter** A function parameter whose value is copied into a parameter variable of a function. If a variable is passed as a value parameter, changes made to the parameter variable inside the function do not affect the original variable outside the program.

**Variable** A storage location that can hold different values.

**Vector** The standard C++ template for a dynamically-growing array.

**Virtual function** A function that can be redefined in a derived class. The actual function called depends on the type of the object on which it is invoked at run time.

**void** A reserved word indicating no type or an unknown type.

**Walkthrough** Simulating a program or a part of a program by hand to test for correct behavior.

**White space** A sequence consisting of space, tab, and/or newline characters.

- _ (underscore), in variable names, 33
- [ ] operator
  - accessing array elements, 252
  - accessing individual string characters, 322–323
- ; (semicolon)
  - in class definitions, 395
  - ending C++ statements, 13
  - in if statements, 80
  - omitting, 14
- \0, null terminator, 321

## A

- \a (alert escape sequence), 493r
- abs function, 43r, 495
- absolute path names, embedding, 482
- absolute values, calculating, 43r
- accessor functions, declaring, 402–403
- accessors, definition, 393–394
- account.cpp (ch05), 223–224
- accounts.cpp (ch07), 312
- adapters, string streams, 363
- adapting algorithms, 269–274
- addition. See also summing
  - + (arithmetic operator), 40, 105r
- Adelman, Leonard, 368
- advisory messages. See error messages
- aggregation relationships, 414–415
- airport luggage handling system, 89
- alert escape sequence (\a), 493r
- algorithms. See also array algorithms; loops; common algorithms
  - adapting, 269–274
  - defining characteristics, 19
  - describing with pseudocode, 18, 20–21
  - designing, 17–21
  - discovering, 274–277
  - encryption, 368
  - executable, 19
  - terminating, 19
  - unambiguous, 19
- aligning
  - file stream output, 361
  - if statements, 81
- Altair 8800, 230
- ambiguity, algorithms, 19
- ampersand (&)
  - address operator, 309
  - reference parameter indicator, 222, 266
- Analytical Engine, 290
- AND operator (&&)
  - confusing with || (OR), 107
  - description, 105r
  - inverting, 108
  - short-circuit evaluation, 108
- ANSI (American National Standards Institute), 7
- Apple II, 230
- Apple Macintosh, 231
- applications
  - baby-name program, 354–357
  - bank account withdrawal simulation, 220–225
  - bell-curve distribution, simulating, 329–332
  - cash register simulation, 400–402, 418–421
  - check-printing program, 211–215
  - coffee-making simulation, 210–211
  - converting numbers to words, 211–215
  - elevator floor simulation, 76–78, 110–111
  - file encryption, 366–367
  - Galton board simulation, 329–332
  - income tax simulation, 94–96
  - input validation with if statements, 109–111
  - investment program, 17–18, 132–136
  - Monte Carlo method, simulation, 170–172
  - printing a table, 165–168
  - quiz scoring program, 269–274
  - quiz-taking program, 443–446, 452–455, 459–462
  - Richter scale program, 90–92
  - triangle pattern program, 227–229
  - vending machine simulation, 54–56
  - world population density, 369–371
- applications, volume calculations
  - bottles, 30–51
  - cans, 30–51
  - cubes, 196–198, 204
  - pyramids, 204–205
  - soft drink containers, 30–51
- arguments, command line, 365–367
- arguments, functions
  - definition, 195
  - modifying, 220–225
  - passing, 199–201
- arithmetic. See also number types
  - `<cmath>` header, 45
  - combining with assignment, 47
  - decrementing variables, 40
  - incrementing variables, 40
  - missing `<cmath>` header, 45
  - rounding floating-point numbers, 41
  - roundoff errors, 45–46
  - unbalanced parentheses, 42
