
## Figure 3.2 How memory changes during variable assignment

![](img/e84ad11adb18201d71595b31ce6c9eff_33_0.png)

- A reserved word cannot be used as an identifier (see Table 3.1).

Here are some examples of valid and invalid identifiers:

- All of the following words are valid identifiers and so qualify as variable names: x, x2, total, port_22, and FLAG.

- None of the following words are valid identifiers: sub-total (dash is not a legal symbol in an identifier), first entry (space is not a legal symbol in an identifier), 4all (begins with a digit), #2 (pound sign is not a legal symbol in an identifier), and class (class is a reserved word).

C++ reserves a number of words for special use that could otherwise be used as identifiers. Called reserved words or keywords, these words are special and are used to define the structure of C++ programs and statements. Table 3.1 lists all the C++ reserved words.

The purposes of many of these reserved words are revealed throughout this book.

You may not use any of the reserved words in Table 3.1 as identifiers. Fortunately, if you accidentally attempt to use one of the reserved words in a program as a variable name, the compiler will issue an error (see Section 4.6 for more on compiler errors).

In Listing 2.1 (simplecpp) we used several reserved words: using, namespace, and int. Notice that include, cout, and main are not reserved words.

Some programming languages do not require programmers to declare variables before they are used; the type of a variable is determined by how the variable is used. Some languages allow the same variable

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

- When variables must be declared, the compiler can catch typographical errors that dynamically-typed languages cannot detect. For example, consider the following section of code:

```
int ZERO;
ZERO = 1;
```

The identifier in the first line ends with a capital “O.” In the second line, the identifier ends with the digit zero. The distinction may be difficult or impossible to see in a particular editor or printout of the code. A C++ compiler would immediately detect the typo in the second statement, since ZERO (last letter a zero) has not been declared. A dynamically-typed language would create two variables: ZERO and ZERO0.

- When variables must be declared, the compiler can catch invalid operations. For example, a variable may be declared to be of type int, but the programmer may accidentally assign a non-numeric value to the variable. In a dynamically-typed language, the variable would silently change its type introducing an error into the program. In C++, the compiler would report the improper assignment as error, since once declared a C++ variable cannot change its type.

- Ideally, requiring the programmer to declare variables forces the programmer to plan ahead and think more carefully about the variables a program might require. The purpose of a variable is tied to its type, so the programmer must have a clear notion of the variable’s purpose before declaring it. When variable declarations are not required, a programmer can “make up” variables as needed as the code is written. The programmer need not do the simple double check of the variable’s purpose that writing the variable’s declaration requires. While declaring the type of a variable specifies its purpose in only a very limited way, any opportunity to catch such errors is beneficial.

- Statically-typed languages are generally more efficient than dynamically-typed languages. The compiler knows how much storage a variable requires based on its type. The space for that variable’s value will not change over the life of the variable, since its type cannot change. In a dynamically typed language that allows a variable to change its type, if a variable’s type changes during program execution, the storage it requires may change also, so memory for that variable must be allocated elsewhere to hold the different type. This memory reallocation at run time slows down the program’s execution.

C++ is a case-sensitive language. This means that capitalization matters. if is a reserved word, but none of IF, If, or iF are reserved words. Identifiers are case sensitive also; the variable called Name is different from the variable called name.

Since it can be confusing to human readers, you should not distinguish variables merely by names that differ in capitalization. For the same reason, it is considered poor practice to give a variable the same name as a reserved word with one or more of its letters capitalized.

## 3.4 Additional Integer Types

C++ supports several other integer types. The type short int, which may be written as just short, represents integers that may occupy fewer bytes of memory than the int type. If the short type occupies less memory, it necessarily must represent a smaller range of integer values than the int type. The C++ standard does not require the short type to be smaller than the int type; in fact, they may represent the same set of integer values. The long int type, which may be written as just long, may occupy more storage than the int type and thus be able to represent a larger range of values. Again, the standard does not require the long type to be bigger than the int type. Finally, the long long int type, or just long long, may be larger than a long. The C++ standard guarantees the following relative ranges of values hold:

```
short int ≤ int ≤ long int ≤ long long int
```

On a small embedded device, for example, all of these types may occupy the exact same amount of memory and, thus, there would be no advantage of using one type over another. On most systems, however, there will be some differences in the ranges.

C++ provides integer-like types that exclude negative numbers. These types include the word unsigned in their names, meaning they do not allow a negative sign. The unsigned types come in various potential sizes in the same manner as the signed types. The C++ standard guarantees the following relative ranges of unsigned values:

```
unsigned short ≤ unsigned ≤ unsigned long ≤ unsigned long long
```

Table 3.2 lists the differences among the signed and unsigned integer types in Visual C++. Notice that the corresponding signed and unsigned integer types occupy the same amount of memory. As a result, the unsigned types provide twice the range of positive values available to their signed counterparts. For applications that do not require negative numbers, the unsigned type may be a more appropriate option.
