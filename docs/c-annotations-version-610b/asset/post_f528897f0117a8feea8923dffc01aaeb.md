
Many readers have submitted suggestions for improvements since version 8.3.1 was released. A big ‘thank you’ to all of you, but in particular to **Francesco Poli** who continued to send in suggestions for improvements for a period of almost two years. His suggestions were an invaluable source of improvement for almost every single section of the C++ Annotations. Thanks, Francesco, for all the effort you've put in improving this document!

Finally, in version 9.0.0 sections were added and sometimes moved. The section about *unrestricted unions* was completed and moved to the 'Containers' chapter, and a new section about adding binary operators to classes using function templates was added to the C++ Annotations' final chapter (concrete examples).

- **Version 8.3.1:** usually a subminor version isn't explicitly mentioned in this section, but in this case the changes from 8.3.0 to 8.3.1 were the result of many, many small and not so small corrections submitted by Francesco Poli who did a very thorough close reading job on the Annotations. Thanks again, Francesco, for all your contributions!
- **Version 8.3.0** adds sections about various (member) function adaptors and adds/rephrases several sections about statistical distribution functions (chapter **18**). When covering elements from the C++0x standard it is assumed that the GNU g++ compiler version 4.4 is available. With elements of the C++0x standard requiring versions beyond 4.4 the required versions are explicitly mentioned, if already known. All suggestions sent in by various readers have also been processed, their help to improve the quality of the C++ Annotations is greatly appreciated: thanks!
- **Version 8.2.0** adds a section about casting `shared_ptrs` (section **18.4.5**) and about sharing arrays of objects (**18.4.6**).
- **Version 8.1.0** was released following a complete overhaul of the C++ Annotations, with two pre-releases in between. Many inconsistencies that had crept into the text and examples were removed, streamlining the text and synchronizing examples with the text. All of the code examples have received a work-over, replacing `endl` by `'\n'`, making virtual functions private, etc. The sections labeled C++11 were improved and sections showing C++11 now also mention the g++ version in which the new feature would be made available, using ? if this is as yet unknown. No version is shown if the feature is already available in g++ 4.3 (or in one of its subreleases, like 4.3.3). I received a host of suggestions from Francesco Poli (thanks, Francesco (and several others), for all the effort you've put into sending me those corrections).
- **Version 8.0.0** was released as a result of the upcoming new C++ standard^4 becoming (partially) available in the GNU g++ compiler^5. Not all new elements of the new standard (informally called the C++0x standard) are available right now, and new subreleases of the C++ Annotations will appear once more elements become implemented in the g++ compiler. In section **2.2.3** the way to activate the new standard is shown, and new sections covering elements of the new standard show C++11 in their section-titles.

Furthermore, two new chapters were added: the STL chapter is now split in two. The STL chapter now covers the STL except for the *Generic Algorithms* which are now discussed in a separate chapter. Name spaces, originally covered by the introductory chapter are now also covered in a separate chapter.

## 2.2 C++'s history

The first implementation of C++ was developed in the 1980s at the AT&T Bell Labs, where the Unix operating system was created.

C++ was originally a 'pre-compiler', similar to the preprocessor of C, converting special constructions in its source code to plain C. Back then this code was compiled by a standard C compiler. The 'pre-code', which was read by the C++ pre-compiler, was usually located in a file with the extension `.c`, `.C` or `.cpp`. This file would then be converted to a C source file with the extension `.c`, which was thereupon compiled and linked.

The nomenclature of C++ source files remains: the extensions .cc and .cpp are still used. However, the preliminary work of a C++ pre-compiler is nowadays usually performed during the actual compilation process. Often compilers determine the language used in a source file from its extension. This holds true for Borland's and Microsoft's C++ compilers, which assume a C++ source for an extension .cpp. The GNU compiler g++, which is available on many Unix platforms, assumes for C++ the extension .cc.

The fact that C++ used to be compiled into C code is also visible from the fact that C++ is a superset of C: C++ offers the full C grammar and supports all C-library functions, and adds to this features of its own. This makes the transition from C to C++ quite easy. Programmers familiar with C may start `programming in C++` by using source files having extensions .cc or .cpp instead of .c, and may then comfortably slip into all the possibilities offered by C++. No abrupt change of habits is required.

### 2.2.1 History of the C++ Annotations

The original version of the C++ Annotations was written by Frank Brokken and Karel Kubat in Dutch using LaTeX. After some time, Karel rewrote the text and converted the guide to a more suitable format and (of course) to English in September 1994.

The first version of the guide appeared on the net in October 1994. By then it was converted to SGML. Gradually new chapters were added, and the contents were modified and further improved (thanks to countless readers who sent us their comments).

In major version four Frank added new chapters and converted the document from SGML to yodl^6.

> **The C++ Annotations are freely distributable. Be sure to read the legal notes^7.**
>
> **Reading the annotations beyond this point implies that you are aware of these notes and that you agree with them.**

If you like this document, tell your friends about it. Even better, let us know by sending email to Frank^8.

In the Internet, many useful hyperlinks exist to C++. Without even suggesting completeness (and without being checked regularly for existence: they might have died by the time you read this), the following might be worthwhile visiting:

- http://www.cplusplus.com/ref/: a reference site for C++.
- http://www.csci.csusb.edu/dick/c++std/cd2/index.html: offers a version of the 1996 working paper of the C++ ANSI/ISO standard.

### 2.2.2 Compiling a C program using a C++ compiler

Prospective C++ programmers should realize that C++ is not a perfect superset of C. There are some differences you might encounter when you simply rename a file to a file having the extension .cc and run it through a C++ compiler:

- In C, `sizeof('c')` equals `sizeof(int)`, `'c'` being any ASCII character. The underlying philosophy is probably that `char`s, when passed as arguments to functions, are passed as integers anyway. Furthermore, the C compiler handles a character constant like `'c'` as an integer constant. Hence, in C, the function calls

    ```c
    putchar(10);
    ```

    and

    ```c
    putchar('\n');
    ```

    are synonymous.

    By contrast, in **C++**, `sizeof('c')` is always 1 (but see also section [3.4.2](#)). An int is still an int, though. As we shall see later (section [2.5.4](#)), the two function calls

    ```c
    somefunc(10);
    ```

    and

    ```c
    somefunc('\n');
    ```

    may be handled by different functions: **C++** distinguishes functions not only by their names, but also by their argument types, which are different in these two calls. The former uses an `int` argument, the latter a `char`.

- **C++ requires very strict prototyping of external functions.** E.g., in C a prototype like

    ```c
    void func();
    ```

    means that a function `func()` exists, returning no value. The declaration doesn't specify which arguments (if any) are accepted by the function.

    However, in C++ the above declaration means that the function `func()` does *not* accept any arguments at all. Any arguments passed to it result in a compile-time error.

    Note that the keyword `extern` is not required when declaring functions. A function definition becomes a function declaration simply by replacing a function's body by a semicolon. The keyword `extern` *is* required, though, when declaring variables.

### 2.2.3 Compiling a C++ program

To compile a **C++** program, a **C++** compiler is required. Considering the free nature of this document, it won't come as a surprise that a *free compiler* is suggested here. The Free Software Foundation (FSF) provides at `http://www.gnu.org` a free **C++** compiler which is, among other places, also part of the Debian (`http://www.debian.org`) distribution of Linux (`http://www.linux.org`).

C++'s C++11 standard (also known as the C++0x standard) has not yet fully been implemented in the g++ compiler. Unless indicated otherwise, all features of the C++11 standard covered by the **C++** Annotations are available in g++ 4.6.

To use these features the compiler flag `-std=c++0x` must currently be provided. It is assumed that this flag is used when compiling the examples given by the Annotations. The features of the C++11 standard may or may not be available in g++ versions before 4.6.

In addition to the `-std=c++0x` compiler flag, g++ 4.7 and beyond also offer the `-std=c++11` flag.

### 2.2.3.1 C++ under MS-Windows

For MS-Windows Cygwin (`http://sources.redhat.com/cygwin`) provides the foundation for installing the *Windows port* of the GNU g++ compiler.

When visiting the above URL to obtain a free g++ compiler, click on `install now`. This will download the file `setup.exe`, which can be run to install Cygwin. The software to be installed can be downloaded by `setup.exe` from the internet. There are alternatives (e.g., using a CD-ROM), which are described on the Cygwin page. Installation proceeds interactively. The offered defaults are sensible and should be accepted unless you have reasons to divert.

^4 http://en.wikipedia.org/wiki/C++11
^5 http://gcc.gnu.org/projects/cxx0x.html
^6 http://ydl.sourceforge.net
^7 legal.shtml
^8 mailto:fb.broken@rug.nl
