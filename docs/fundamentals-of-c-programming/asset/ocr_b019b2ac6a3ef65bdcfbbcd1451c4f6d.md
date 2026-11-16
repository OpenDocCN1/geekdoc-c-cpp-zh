| alignas | decltype | namespace | struct |
| :--- | :--- | :--- | :--- |
| alignof | default | new | switch |
| and | delete | noexcept | template |
| and_eq | double | not | this |
| asm | do | not_eq | thread_local |
| auto | dynamic_cast | nullptr | throw |
| bitand | else | operator | true |
| bitor | enum | or | try |
| bool | explicit | or_eq | typedef |
| break | export | private | typeid |
| case | extern | protected | typename |
| catch | false | public | union |
| char | float | register | unsigned |
| char16_t | for | reinterpret_cast | using |
| char32_t | friend | return | virtual |
| class | goto | short | void |
| compl | if | signed | volatile |
| const | inline | sizeof | wchar_t |
| constexpr | int | static | while |
| const_cast | long | static_assert | xor |
| continue | mutable | static_cast | xor_eq |

Table 3.1: C++ reserved words. C++ reserves these words for specific purposes in program construction. None of the words in this list may be used as an identifier; thus, you may not use any of these words to name a variable.

to assume different types as its use differs in different parts of a program. Such languages are known as dynamically-typed languages. C++ is a statically-typed language. In a statically-typed language, the type of a variable must be explicitly specified before it is used by statements in a program. While the requirement to declare all variables may initially seem like a minor annoyance, it offers several advantages:

+   - When variables must be declared, the compiler can catch typographical errors that dynamically-typed languages cannot detect. For example, consider the following section of code:
+   
+   ```
+   int ZERO;
+   ZERO = 1;
+   ```

The identifier in the first line ends with a capital “O.” In the second line, the identifier ends with the digit zero. The distinction may be difficult or impossible to see in a particular editor or printout of the code. A C++ compiler would immediately detect the typo in the second statement, since ZERO (last letter a zero) has not been declared. A dynamically-typed language would create two variables: ZERO and ZERO0.

+   - When variables must be declared, the compiler can catch invalid operations. For example, a variable may be declared to be of type int, but the programmer may accidentally assign a non-numeric value to the variable. In a dynamically-typed language, the variable would silently change its type introducing an error into the program. In C++, the compiler would report the improper assignment as error, since once declared a C++ variable cannot change its type.

+   - Ideally, requiring the programmer to declare variables forces the programmer to plan ahead and think more carefully about the variables a program might require. The purpose of a variable is tied to its type, so the programmer must have a clear notion of the variable’s purpose before declaring it. When