control structures. C may be termed as a mid-level language, not as low-level as assembly and not as high-level as BASIC. C is a high-level language which also provides the capabilities that enable the programmers to 'get close' with the hardware and allows them to interact with the computer on a much lower level.

# ### 8.1.1 Why Learn C?

There are a large number of programming languages in the world today—C++, Java, Ada, BASIC, COBOL, Perl, Pascal, Smalltalk, FORTRAN, etc. Even so, there are several reasons to learn C, some of which are stated as follows.

**C is a core language** In computing, C is a general-purpose, cross-platform, block structured, procedural, imperative computer programming language. A number of common and popular computer languages are based on C. Having learnt C, it will be much easier to learn languages that are largely or in part based upon C. Such languages include C++, Java, and Perl.

**C is a small language** C has only thirty-two keywords and only about twenty of them are in common use. This makes it relatively easy to learn compared to bulkier languages.

**C is quick** We can write codes which run quickly, and the program can be very 'close to the hardware'. This implies that you can access low-level facilities in your computer quite easily, without the compiler or run-time system stopping you from doing something potentially dangerous.

**C is portable** C programs written on one system can be run with little or no modification on other systems. If modifications are necessary, they can often be made by simply changing a few entries in a header file accompanying the main program. The use of compiler directives to the preprocessor makes it possible to produce a single version of a program which can be compiled on several different types of computer. In this sense, C is said to be very portable. The function libraries are standard for all versions of C so they can be used on all systems.

# ### 8.1.2 The Future of C

The story about C is not yet over. During the time when the X3J11 committee moved steadily towards producing the ANSI C standard, another researcher, Bjarne Stroustrup of Bell Laboratories began experimenting with an object-oriented flavour of C that he called C++ (pronounced C plus plus). C++ extended C, and according to Stroustrup, refined the language, making C++, in his words, 'a better C'.

Apparently, the X3J11 committee agreed, if not completely, and they adopted some of Stroustrup's proposals into the ANSI C standard. Subsequently, a new committee was formed to investigate a standard for ANSI C++ that is now ready. Does this new standard mean that ANSI C is destined to join its ancestors BCPL, B, and K&R C on the heap of discarded programming languages?

The answer is a solid no. Frankly, C++ is not for everyone. When learning C, it is best to stick to the basics, and readers would be well advised to ignore some of the more advanced elements found in C++. For example, C++ provides classes for *object-oriented programming*, or OOP as it is known. Until one knows C, one is not ready for OOP.

On the other hand, because C++ is based on ANSI C, one may as well use modern next-generation C++ compilers to write C programs. That way, one can take advantage of both worlds. After learning C, one is ready to tackle OOP and other advanced C++ subjects.

# ## 8.2 STANDARDIZATIONS OF C LANGUAGE

Both UNIX and C were created at AT&T's Bell Laboratories in the late 1960s and early 1970s. During the 1970s the C programming language became increasingly popular. Many universities and organizations began creating their own variations of the language for their own projects.

During the late 1970s and 1980s, various versions of C were implemented for a wide variety of mainframe computers, minicomputers, and microcomputers, including the IBM PC. In the early 1980s, a need was realized to standardize the definition of the C language which in turn would help C become more widespread in commercial programming.

In 1983, the American National Standards Institute (ANSI) formed a committee to establish a standard specification of C known as 'ANSI C'. This work ended in the creation of the so-called C89 standard in 1989. Part of the resulting standard was a set of software libraries called the ANSI C standard library. This version of the language is often referred to as ANSI C, Standard C, or sometimes C89. ISO/IEC standard was thereafter adopted by ANSI and people referred to this common standard as simply 'standard' or simply 'C89'.

In 1990, the ANSI C standard (with a few minor modifications) was made by the International Organization for Standardization (ISO) as ISO/IEC 9899:1990. This version is sometimes called C90. Therefore, the terms 'C89' and 'C90' refer to essentially the same language.

Changes included in C89 are as follows:

+   - The addition of truly standard library
+   - New preprocessor commands and features
+   - Function prototypes which specify the argument types in a function declaration
+   - Some new keywords const, volatile, and signed
+   - Wide characters, wide strings, and multi-byte characters
+   - Many smaller changes and clarification to conversion rules, declarations, and type checking

C89 is supported by current C compilers, and most C code being written nowadays is based on it. In 1995, amendments to C89 include