
### thrd_t
Line 26 creates an array of thrd_t objects. When you create a thread, the multithreading library creates a thread ID and stores it in a thrd_t object. The thread's ID can then be used with various multithreading functions.

### Creating and Executing a Thread
Lines 31–41 create two threads by calling function thrd_create (line 36). The function's three arguments are:
- A thrd_t pointer that thrd_create uses to store the thread's ID.
- A pointer to a function (startFibonacci) that specifies the task to perform in the thread. The function must return an int and receive a void pointer representing the argument to the function (in this case, a pointer to a ThreadData object). The int represents the thread's state when it terminates (e.g., thrd_success or thrd_error).
- A void pointer to the argument that should be passed to the function in the second argument.

Function thrd_create returns thrd_success if the thread is created, thrd_nomem if there was not enough memory to allocate the thread or thrd_error otherwise. If the thread is created successfully, the function specified as the second argument begins executing in the new thread.

### Joining the Threads
To ensure that the program does not terminate until the threads terminate, lines 44–45 call thrd_join for each thread that we created. This causes the program to wait until the threads complete execution before executing the remaining code in main. Function thrd_join receives the thrd_t representing the ID of the thread to join and an int pointer where thrd_join can store the status returned by the thread. After the threads terminate, lines 48–57 calculate and display the total execution time by determining the time difference between the time the first thread started and the second thread ended.

### Function startFibonacci
Function startFibonacci (lines 61–77) specifies the task to perform—in this case, to call fibonacci to recursively perform a calculation, to time the calculation, to display the calculation's result and to display the time the calculation took (as we did in Fig. E.11). The thread executes until startFibonacci returns the thread's status (thrd_success, line 76), at which point the thread terminates.

### Other C11 Multithreading Features
In addition to the basic multithreading support shown in this section, C11 also includes other features such as _Atomic variables and atomic operations, thread local storage, conditions and mutexes. For more information on these topics, see Sections 6.7.2.4, 6.7.3, 7.17 and 7.26 of the standard and the following blog post and article:

http://blog.smartbear.com/software-quality/bid/173187/C11-A-New-C-Standard-Aiming-at-Safer-Programming
http://lwn.net/Articles/508220/

## E.9.3 quick_exit function
In addition to exit (Section 14.6) and abort, C11 now also supports function quick_exit (header <stdlib.h>) for terminating a program. Like exit, you call quick_exit and pass it an exit status as an argument—typically EXIT_SUCCESS or EXIT_FAILURE, but other platform-specific values are possible. The exit status value is returned from the program to the calling environment to indicate whether the program terminated successfully or an error occurred. When called, quick_exit can, in turn, call up to at least 32 other functions to perform clean-up tasks. You register these functions with the at_quick_exit function (similar to atexit in Section 14.6) and are called in the reverse order from which they were registered. Each registered function must return void and have a void parameter list. The motivation for functions quick_exit and at_quick_exit is explained at

http://www.open-std.org/jtc1/sc22/wg14/www/docs/n1327.htm

## E.9.4 Unicode® Support
Internationalization and localization is the process of creating software that supports multiple spoken languages and locale-specific requirements—such as displaying monetary formats. The Unicode® character set contains characters for many of the world's languages and symbols. C11 now includes support for both the 16-bit (UTF-16) and 32-bit (UTF-32) Unicode character sets, which makes it easier for you to internationalize and localize your apps. Section 6.4.5 in the C11 standard discusses how to create Unicode string literals. Section 7.28 in the standard discusses the features of the new Unicode utilities header (<uchar.h>), which include the new types char16_t and char32_t for UTF-16 and UTF-32 characters, respectively. At the time of this writing, the new Unicode features are not widely supported among C compilers.

## E.9.5 _Noreturn Function Specifier
The _Noreturn function specifier indicates that a function will not return to its caller. For example, function exit (Section 14.6) terminates a program, so it does not return to its caller. Such functions in the C Standard Library are now declared with _Noreturn. For example, the C11 standard shows function exit's prototype as:

```
_Noreturn void exit(int status);
```

If the compiler knows that a function does not return, it can perform various optimizations. It can also issue error messages if a _Noreturn function is inadvertently written to return.

## E.9.6 Type-Generic Expressions
C11's new _Generic keyword provides a mechanism that you can use to create a macro (Chapter 13) that can invoke different type-specific versions of functions based on the macro's argument type. In C11, this is now used to implement the features of the type-generic math header (<tgmath.h>). Many math functions provide separate versions that take as arguments floats, doubles or long doubles. In such cases, there is a macro that automatically invokes the corresponding type-specific version. For example, the macro ceil invokes the function ceilf when the argument is a float, ceil when the argument is a double and ceill when the argument is a long double. Section 6.5.1.1 of the C11 standard discusses the details of using _Generic.

## E.9.7 Annex L: Analyzability and Undefined Behavior
The C11 standard document defines the features of the language that compiler vendors must implement. Because of the extraordinary range of hardware and software platforms and other issues, the standard specifies in a number of places that the result of an operation is undefined behavior. These can raise security and reliability concerns—every time there's an undefined behavior something happens that could leave a system open to attack or failure. The term "undefined behavior" appears approximately 50 times in the C11 standard document.

The people from CERT (cert.org) who developed C11's optional Annex L on analyzability scrutinized all undefined behaviors and discovered that they fall into two categories—those for which compiler implementers should be able to do something reasonable to avoid serious consequences (known as bounded undefined behaviors), and those for which implementers would not be able to do anything reasonable (known as critical undefined behaviors). It turned out that most undefined behaviors belong to the first category. David Keaton (a researcher from the CERT Secure Coding Program) explains the categories in the following article:

http://blog.sei.cmu.edu/post.cfm/improving-security-in-the-latest-c-programming-language-standard-1

The C11 standard's Annex L identifies the critical undefined behaviors. Including this annex as part of the standard provides an opportunity for compiler implementors—a compiler that's Annex L compliant can be depended upon to do something reasonable for most of the undefined behaviors that might have been ignored in earlier implementations. Annex L still does not guarantee reasonable behavior for critical undefined behaviors. A program can determine whether the implementation is Annex L compliant by using conditional compilation directives (Section 13.5) to test whether the macro __STDC_ANALYZABLE__ is defined.

## E.9.8 Memory Alignment Control
In Chapter 10, we discussed the fact that computer platforms have different boundary alignment requirements, which could lead to struct objects requiring more memory than the total of their members' sizes. C11 now allows you to specify the boundary alignment requirements of any type using features of the <stdalign.h> header. _Alignas is used to specify alignment requirements. Operator alignof returns the alignment requirement for its argument. Function aligned_alloc allows you to dynamically allocate memory for an object and specify its alignment requirements. For more details see Section 6.2.8 of the C11 standard document.

## E.9.9 Static Assertions
In Section 13.10, you learned that C's assert macro tests the value of an expression at execution time. If the condition's value is false, assert prints an error message and calls function abort to terminate the program. This is useful for debugging purposes. C11 now provides _Static_assert for compile-time assertions that test constant expressions after the preprocessor executes and at a point during compilation when the types of expressions are known. For more details see Section 6.7.10 of the C11 standard document.
