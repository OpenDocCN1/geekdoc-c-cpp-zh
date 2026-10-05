Explanation: Not required.

+   33. b

Explanation: The extern is just as a declaration and expect the definition of the variable later in the program (linking phase). Its resolution takes place during the scanning of symbols, and symbol table creation. The extern specifies that the definition for the extern type variable is present in some other programs/library or in the same program as a global variable. The given program compiles correctly but when the resolution of ‘p’ comes, it checks in other associated files, library files for the definition of variable ‘p’. But it would not find any definition of ‘p’ because it is just a variable name, not any keyword. Linker link-time error gets thrown by the compiler. Linker Error : Undefined symbol ‘p’.

+   34. b

Explanation: The ‘p’ is not an external variable, so the compiler will check from the symbol table and throws an error that ‘p’ is not declared. If we use extern it means that compiler skips and waits ’ we use extern it means that compiler skips and waits the linking phase for resolving p.

+   35. a

Explanation: It works fine, the resolution of ‘p’ will not take place at compile-time, it takes place during link time. The definition of ‘p’ is present in the symbol table. Hence, the value of ‘p’ can be directly resolved during link time.

+   36. d

Explanation: It's a concept of the void pointer, we already discussed it in explanation of questions 3, 4, 29.

+   37. d

Explanation: One more flavor of switch statement we have discussed in the explanation of questions 20 and 22.

+   38. d

Explanation: A simple recursive program, explanation not required.

+   39. c