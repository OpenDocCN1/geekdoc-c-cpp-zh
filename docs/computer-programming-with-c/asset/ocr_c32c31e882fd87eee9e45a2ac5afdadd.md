The statement includes the contents of the header file `iostream.h` into the program, so as to facilitate the programmer to use the built-in object of class `ostream`, which is named as `cout` directly in the code. Remember, `#include` is a pre-processor directive, which is used to include the contents of a particular header file into the C++ program before the compilation of the code starts. This ensures that the complete definition of the class `ostream` and the insertion operator `<<` is included in the program before the compilation. Details about classes and objects are discussed in Chapter 11 of this text book. **The only point we must understand at this stage is that the statement**

`cout<<"I like Computer Programming";`

*is used to print a message as I like Computer Programming on the computer screen as shown in Figure 2.4. And we must include the contents of header file `iostream.h` before making use of `cout` in our program.*

![](bbox=[0.157, 0.367, 0.817, 0.573])

**Figure 2.4:** Usage of cout

C++ supports *streaming outputs*, which are not supported by C. In general, the word *stream* refers to the flow of data in the computer system. The *output stream* of C++ allows the programmer to perform a ‘write’ operation on the output devices such as ‘screen’, ‘file’, and ‘disk’. The header file `iostream.h` defines the necessary classes and functions to support the streaming input and output. We will discuss the *input streams* of C++ in the later sections of this chapter. As we have written the `cout` instruction inside the main function, the processor will now execute the instruction after translating the instruction into a machine code, thereby printing a message specified on the computer screen as seen in the output of the program.

# NOTES

The program given in Figure 2.2 uses `printf()` statement to print a message on the computer screen. The `printf()` function is declared in header file `stdio.h` which is included in the program. The program using `printf()` works with C as well as C++ because the header file `stdio.h` and `printf()` function are supported by both the languages. However, the program using `cout` shown in Figure 2.3 works with C++ but not with C. This is because the object `cout` and header file `iostream.h` are only supported by C++ and not by C. This clearly means that C++ supports streaming output operations whereas C does not. We will learn more about streams supported by C++ in Chapter 15.