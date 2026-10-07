
75. When you pass an array name as a function argument, are you passing it by value, reference, or address?

76. What is a pointer?

77. What is the difference between declaring an integer variable and declaring an integer pointer variable?

78. What is the meaning of the data type in the declaration of a pointer?

79. What is the meaning and purpose of NULL when being assigned to a pointer?

80. What operator do you use to assign a pointer the address of another variable or constant?

81. What is the purpose of the indirection operator?

82. What is the effect of incrementing a pointer variable?

83. What are the purposes of the *new* and delete operators?

84. Can you use an assignment operator to assign the value of one C-string to another?

85. What does it mean for data to be persistent?

86. What is a file?

87. What standard library should you include when your program reads from, or writes to, files?

88. Which of the three objects, *fstream*, *iostream*, or *ofstream*, may be used both for file input and output?

89. What are the two functions you can use to open a file?

90. What is the purpose of opening a file?

91. What is the purpose of closing a file?

92. What is a constructor?

93. Should file stream objects be passed as function arguments by value or by reference?

94. What type of relationship is involved in inheritance?

95. What type of relationship is involved in containership?

96. What is a structure?

97. What are the two ways to initialize a structure?

98. Can you nest one structure within another structure?

99. Why may a structure be passed by reference if the function will not change the value of its member variables?

100. What is an important difference between a structure and a class?

# Answers to Quizzes and Final Exam

## Chapter 1

- 1. A computer program consists of step-by-step instructions to the computer from a computer programmer.
- 2. Computers can store greater amounts of information, can recall that information more quickly and accurately, and can perform calculations faster and more accurately.
- 3. A programming language is a language that resembles the structure and syntax of human language, and is used by computer programmers to write instructions for computers.
- 4. C++ is a good programming language to learn because it is widely used in industry and, also because many other programming languages, including Java and C#, are based on C++.
- 5. A function is a group of related instructions, also called statements, which together perform a particular task.
- 6. A C++ program must have one main function, no more, no less.
- 7. A standard library file is a file that defines commonly used objects, such as cout.
- 8. The purpose of an include directive is to tell the program to include a particular standard library file in your application.
- 9. A preprocessor is a processor that scans the source code for include directives, and then inserts them into the source code of all files included by the preprocessor.
- 10. The compiler is a program that translates the preprocessed source code to the source code after the insertions made by the preprocessor into corresponding machine language instructions that are stored in an object file.
- 11. The linker is a program that combines the object file with the necessary parts of the runtime library and creates an executable file.

## Chapter 2

- 1. The CPU can most quickly access instructions or data from cache memory that is on the CPU itself.
- 2. Persistent storage is not temporary like the other two: cache memory and RAM.
- 3. One byte of information may be stored at a particular memory address.
- 4. No size of a data type may vary depending on the compiler and operating system.
- 5. The range of a data type is the highest and lowest value that that data type may represent.
- 6. The value of an unsigned data type is either zero or positive, never negative, whereas the value of a signed data type may be negative also.
- 7. .0051 is represented by 5.1E-3 in E notation.
- 8. An ASCII value is a number between 0 and 255 that corresponds to a particular character.
- 9. The sizeof operator returns the size in bytes of a data type on the compiler and operating system on which the program is running.
- 10. A literal is a string, generally encased in double quotes, that is output literally, without evaluation.
- 11. An expression is a code statement with a value that has to be evaluated when the program runs.

## Chapter 3

- 1. Declaring a variable reserves memory for the storage of information and provides a name by which that information later can be referred to in code.
- 2. No. An "undeclared identifier" compiler error will occur even though the variable is declared after it is referred to because the compiler reads the code from top to bottom, when it reaches the first reference to the variable, it has not seen the variable declaration.
- 3. Yes, as long as the variables are of the same data type.
- 4. A naming convention is a consistent method of naming variables.
- 5. The address operator is used to obtain the hexadecimal value of a variable's memory address, whereas the size of operator is used to determine the number of bytes in memory required to store the variable.
- 6. Initialization is when you assign a value to a variable as part of the same statement that declares that variable.
- 7. Overflow occurs when a variable is assigned a value too large for its range.
- 8. A compiler error is the consequence of using an assignment operator to assign a string value to an integer variable.
- 9. You use the cin object for run-time assignment of values to variables.
- 10. Yes. You can use one cin statement to assign values to several variables of different data types.

## Chapter 4

Division has more than one operator, / and %.

- 1. The addition operator can operate on string as well as numeric operands.
- 2. The modulus operator cannot have a floating point operand.
- 3. The division operators, / and %, cannot have zero as a second operand.
- 4. total += 2
- 5. The result of 2 + 3 * 4 is 14, not 20, because multiplication has precedence over addition.
- 6. The result of the expression 8 / 2 * 4 is 16, not 1, because of associativity. Multiplication and division have equal precedence, so the operations are performed from left to right.
- 7. The result of the expression 10 / 4 is 2, not 2.5, because of integer division.
- 8. C++, unlike some other programming languages, does not have an exponent operator. Instead, use the pow function, defined in the cmath standard library, to raise a number to a certain power.
- 9. An algorithm is a step-by-step logical procedure for solving a problem.

## Chapter 5

- 1. There are two operands in a relational expression.
- 2. The purpose of a flowchart is to visually depict the flow of a program.
- 3. The data type of the expression following the if keyword is Boolean.
- 4. In an if / else if / else statement, you must have one, but only one, if.
- 5. In an if / else if / else statement, you may have more than one else if part.
- 6. In an if / else if / else statement, you may omit the else part, in which case the statement becomes an if/else if statement.
- 7. In a switch statement, the required type of expression following the switch keyword is integer.
- 8. In a switch statement, an expression of the character data type may follow the switch keyword because the ASCII value of a character is an integer.
- 9. In a switch statement, the expression following a case keyword must be a constant and therefore cannot be a variable.
- 10. The default keyword in a switch statement corresponds to the else keyword in an if / else if / else statement.

## Chapter 6

- 1. You can use nested if statements as an alternative to the logical And and Or operators.
- 2. An if statement can be nested in the else if part of an if / else if / else statement, as well as the if part.
- 3. With the logical And operator, both Boolean expressions have to be true for the overall Boolean expression to be true.
- 4. With the logical Or operator, both Boolean expressions have to be false for the overall Boolean expression to be false.
- 5. The logical Not operator reverses the “truth” of a Boolean expression, making a true expression false and a false expression true.
- 6. Assuming resident is a Boolean variable, if(resident) is the same as if(resident == true).
- 7. The logical Not operator is a unary rather than binary operator.
- 8. The logical Not operator has a higher precedence than the relational operators.
- 9. The logical And operator has a higher precedence than the logical Or operator.
- 10. A Boolean value of either true or false can be used following the case keyword in a switch statement since both true and false have corresponding integer values.
