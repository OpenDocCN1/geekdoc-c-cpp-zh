
### 6.5.5 Functions of exit and atexit

- Present the exit function, which ends a program.
- Talk about registering routines to be called at program termination using the atexit function.

### 6.5.6 Function of the System

- Describe the system function that allows a C program to run shell commands from inside it.
- Talk about the system's security implications and other factors.

### 6.5.7 Handling Signals (Raise and Signal)

- To handle signals in a C application, introduce the signal function.
- Talk about raising a signal directly using the raise function.

### 6.5.8 Using getpid and getppid

- Describe the getpid function, which returns the current process's ID.
- To acquire the parent process ID, introduce the getppid function.

### 6.5.9 Function of Abort

- Provide the abort function to end a program unexpectedly.
- Talk about situations in which an abort might be employed.

### 6.5.10 Declare Macro

- Examine the assert macro that was presented in the section on error handling.
- Talk about how it helps with debugging and software development.

### 6.5.11 Function of qsort (Optional)

- Give a brief overview of the qsort function, which sorts arrays.
- Talk about how to customize and utilize it using function pointers.

### 6.5.12 bsearch: An Optional Function

- Explain in brief how to use a sorted array's bsearch function for binary searching.
- Talk about how it may be used for effective searches.

### 6.5.13 Functions putchar_unlocked and getchar_unlocked (Optional)

- Describe the putchar_unlocked and getchar_unlocked functions in brief so that you can input and output characters more quickly.
- Talk about their use in situations when performance matters.

### 6.5.14 Functions for setjmp and longjmp (Optional)

- Describe in brief the non-local jump routines setjmp and longjmp.
- Talk about the uses and factors to take into account.

### 6.5.15 Extra Common Library Features

- Mention a few more common library functions that weren't thoroughly discussed.
- Promote reading through the C Standard Library documentation to get a thorough knowledge.

### 6.5.16 Inclusion of Libraries (#include Directives)

- Talk about using #include directives to include header files.
- Stress how crucial it is to include the headers required for the functions that are utilized in a program.

Comprehending these auxiliary functions expands the C programmer's toolbox and makes it possible for them to efficiently handle a variety of jobs. The information and abilities provided in this part will enable readers to take advantage of these functions in their C applications.

## Chapter 7. Best Practices and Tips

### 7.1 Writing Efficient and Readable Code

Any C program that wants to succeed has to have understandable and efficient code. Enhancing maintainability and cooperation may lead to improved performance. This section will discuss best practices and pointers for building understandable and effective C code.

### 7.1.1 Coding Structure and Organization

- Modularization: Divide your code into discrete functions that are each responsible for a certain job. This improves readability and makes maintenance and debugging simpler. Write functions that are optimized to do a single job effectively rather than ones that are too lengthy.
- File structure: Logically arrange source files, keeping implementation files and headers apart. Make sure all files and folders have consistent names. As a result, finding and comprehending the functions of various project components is made simpler.

### 7.1.2 Characteristic Naming

- Use descriptive and meaningful names for your variables to make them meaningful. Don't use obscure or single-letter names. This makes the code simpler to read and understand, which will make it easier for you and others to understand in the future.
- Clearly Named Functions: Select function names that express their purpose very well. The necessity for lengthy comments to describe a function's purpose is eliminated by a well-named function. When a function returns a value or an object, use a noun; for functions that execute activities, use verbs.

### 7.1.3 Formatting and indentation that is consistent

- Code readability is improved by consistent indentation. Whether using tabs or spaces for indentation, adhere to a consistent style. This helps in seeing the code structure.
- Brace Placement: Make sure your brace placement is constant. Choose one and adhere to it across your codebase: the K&R style (opening brace on the same line) or the Allman style (opening brace on a new line).
- Line Length: To prevent horizontal scrolling, keep line lengths manageable (usually between 80 and 120 characters). Readability is enhanced by this, particularly when comparing code side by side.

### 7.1.4 Remarks and Recordkeeping

- Compose insightful remarks that elucidate the "why" as opposed to the "what." Comments may clarify design choices or offer context for the code, which should be self-explanatory.
- Write Public Interface Documents: Provide clear documentation for your functions' and libraries' public interfaces. This covers any side effects, return values, input parameters, and function prototypes.
- Comment Updates: Continually update comments to take into account code changes. Code comprehension may be harmed by outdated comments, which might be deceptive.

### 7.1.5 Steer clear of magic numbers and hardcodes

- Use Constants: Define constants with meaningful names in your code rather than just utilizing magic numbers directly. This makes the code easier to understand and facilitates future modifications.
- Configuration choices: Steer clear of hardcoding any configuration choices your software may have directly into the code. To increase the flexibility of your software, use configuration files or command-line options.

### 7.1.6 Resolving Errors

- Verify Return Values: Prior to using any function that may fail, make sure to verify its return values. Put in place the proper error-handling procedures, such as errno, global error variables, and error codes returned.
- Develop your application with graceful degradation in mind to manage mistakes. When possible, avoid abruptly terminating programs; instead, provide descriptive error messages to facilitate troubleshooting.

### 7.1.7 Applying the DRY Principle and Reusing Code

- DRY (Don't Repeat Yourself): Steer clear of redundant code. Rather, use functions or macros to contain common functionality. This simplifies the maintenance of your code and eliminates duplication.
- Division of Concerns: Your code should be divided into several modules or layers, each handling a certain task. This facilitates the extension or modification of individual components and encourages the reuse of code.

### 7.1.8 Prudent Optimization

- Profile First: To precisely identify performance bottlenecks, profile your code prior to optimization. Without any speed advantages, premature optimization might result in complicated and difficult to comprehend code.
- Employ Efficient Techniques: For your issue domain, choose effective algorithms. Occasionally, algorithmic enhancements have greater effects than micro-optimizations.

### 7.1.9 Meaningful Commits and Version Control

- Utilize Version Control: Keep track of code modifications by using version control systems such as Git. To track the development of your software, commit changes on a regular basis using insightful commit statements.
- Using branches for experimental or feature-specific development is a good way to branch and tag code. To identify reliable iterations of your program, tag releases.

### 7.1.10 Test-Driven Development (TDD) and Testing

- Create Unit Tests: Put unit tests into practice to confirm that individual components or functions are valid. Automated testing aids in the early detection of regressions during development.
