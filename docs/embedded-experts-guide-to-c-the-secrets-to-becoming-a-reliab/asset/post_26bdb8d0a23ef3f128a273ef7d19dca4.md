
```
* compilation if it is unavailable. */
#ifndef __STDC_IEC_559__
# error IEEE 754 support is required.
#endif
```

Fig 2.5 The preprocessor can be used to check for required floating point support and abort compilation if necessary.

Floating point variables allow a wider range of values to be represented, but if not supported in hardware, this can require the inclusion of large software libraries. It is often impractical to use floating point arithmetic on platforms with limited resources for this reason. Furthermore, there is a significant performance penalty associated with software implementations, which can be several hundred times slower than the corresponding integer operation. As a result, you should avoid using floating point arithmetic when hardware support is not available.

## Endnotes for Chapter 2 - Writing Safer C

- 1 I would say that I know a fair bit about the language – I wouldn’t be writing a book about it if I didn’t. But I certainly don’t consider myself an expert; I am regularly discovering new and unexpected things about the language.

- 2 Complete portability is usually desirable but often not possible; there will almost always be some part of the code that relies on a specific implementation to work.

- 3 They are also broadly compatible; although MISRA C is more restrictive than BARR C, BARR C is written with the intent that it does not contradict anything within MISRA C.

- 4 Tokenisation is a stage of the compilation process used to demarcate and classify the individual parts of each C statement so that they can be correctly compiled. In the same way that a sentence can be analysed in terms of nouns, verbs and other syntactic units, a program can be understood in terms of variables, operators, and other coding units.

- 5 In general, preprocessor directives should not be terminated with a semicolon, particularly #define directives. Doing so may not cause issues for the preprocessor itself but is more likely than not to be a programming error.

- 6 If you require a tab to be encoded within a string or character (there are no other cases where it would be required or even desirable), the correct way to do this is to use the \t escape sequence, ensuring that a tab character is used rather than a series of spaces.

- 7 This is the example given in the C Standard; in my opinion, such a statement, needs to be completely rewritten anyway, since even in its correct form, its intended purpose appears completely undecipherable.

- 8 If you didn’t spot it straight away, the problem is that /* is interpreted by the compiler as opening a comment, rather than as division by a dereferenced pointer.

- 9 Not everyone agrees with this – some people do not use an additional space when declaring variables. There is some merit to this approach, however, it can cause some confusion if the address of the pointed-to variable (i.e., the value of the pointer, rather than value of the referenced variable) needs to be qualified using either const or volatile. Although technically legal according to the C Standard, it is best never to omit the space between the type and the * as this increases confusion further, particularly if you are in the habit of writing multiple declarations at once (a habit that is best avoided) because the pointer-to-part of the declaration is associated with the variable and not the type being pointed to (it has right associativity for the pedantically minded) and it must be included with each variable being declared.

- 10 The C Standard does not actually prevent longer symbol names, but only requires a conforming compiler to consider the first 31 characters when resolving names. Unless you are in the habit of using very long names that look similar, this limit (and whether your particular compiler is affected by it) is unlikely to be an issue.

- 11 A handle is, like a pointer, a type of reference variable. However, unlike pointers, a handle cannot be used to directly access the referenced object. They can be as simple as an array index – although many implementations are considerably more complex. The term is also used to mean an opaque pointer, i.e., a pointer to an object of a type not visible to the current translation unit, conceptually similar to a pointer to void in that it does not point to data that can be used without additional information.

- 12 Both interrupt service routines and callbacks are unusual in that they are not usually called directly and may therefore appear unused to anyone unfamiliar with their purpose. We will explore these special types of function in detail later.

- 13 Prior to the introduction to the typedef keyword, the only way to generate an alias for a type name was to define it using a macro, so historically this follows the case conventions used elsewhere. This technique will still work but using a typedef with lower-case names, is the preferred way to alias type names.

- 14 I have seen comments that add no information whatsoever, including the single word “equation” for something that was quite clearly an equation. While such comments may not be misleading or inaccurate, they add no context which could be useful in understanding the code.

- 15 The const keyword is poorly named; it does not mean the variable is a constant – it roughly translates to “read-only” or, more precisely, “not modifiable through this instance of the variable.” It is even possible to have a variable that is both volatile and const – essentially, this tells the compiler “the value of this variable can change unexpectedly, but you may not generate any code that will cause it to change.” A read-only hardware register is an example of a variable that may be qualified in such a way.

- 16 This statement assigns a constant address to a pointer. Such usage is generally discouraged, but sometimes necessary when writing code that must address a specific memory location directly, such as a hardware register. The use of const in this case ensures that an alternative address cannot be assigned to the pointer later (note that it is on the right of the asterisk). Note also that the constant address needs to be cast to int * before it can be assigned – failing to do so may not prevent the code from working but will likely cause a warning to be issued.

- 17 There is at least one subtle but important difference. Whereas any pointer to a variable may be legally cast to a pointer to void and a pointer to void may be legally cast to a pointer to a variable of the correct type, such casts are undefined behaviour when applied to pointers to functions (a necessity, since there is no guarantee that variables and functions reside in the same memory space; on a simplistic level, a machine based on the von Neumann architecture will store data and instructions in a single memory space and one based on the Harvard architecture will not). A pointer to a function with one signature may, however, be cast to a pointer to a function with a different signature, although attempting to call it with the wrong signature is still undefined behaviour. I’ve never had any reason to perform such a cast, but someone might find this knowledge useful.

- 18 Prior to C99, int was assumed in variable and function declarations if no type was given and thus always optional. Most compilers continue to treat it as implied for backwards compatibility and issue a warning rather than an error – it's still a good idea to state it explicitly. Strictly speaking, short and long are modifiers and not part of the type name, but since the int is usually omitted, they are often thought of as types (there is also a long double type, where the double is not optional).

- 19 C does not actually include a fixed-point type, but they behave in a very similar way to integer types which can, with care, be used as a substitute for a true fixed-point type.

## Chapter 3: Managing Memory

Memory management for embedded systems differs significantly compared with other systems. Embedded systems generally have resource constraints which can cause dynamic memory allocation to fail. Although failure may occur as a result of memory exhaustion, such failures can also occur without dynamic memory allocation being used. Rather, the risk arises as a result of memory fragmentation; specifically, sufficient free memory can be available, but not as a continuous block of the required size. This, rather than the risk of memory exhaustion, is the reason dynamic memory allocation should be avoided in embedded systems. Assuming the system has been designed with sufficient resources, memory allocation is not the problem; it is the subsequent freeing of the memory which causes fragmentation.

There is therefore relatively little memory management to be done in embedded systems and this chapter is arguably poorly named. Memory is statically allocated, except for variables on the call stack; this ensures usage is deterministic and avoids the fragmentation problem. There are, however, times in embedded programming where behaviour similar to dynamic memory allocation is required; although this could be described as a form of dynamic memory allocation, it should be managed in such a way that memory allocation is still static. Furthermore, although memory fragmentation can still occur, it is handled in such a way so as not to cause the issues seen with true dynamic allocation.
