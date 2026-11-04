# # 1

# # Introduction to C

Before getting into the details of C language, this chapter presents, in brief, its history, evolution, strengths, and weaknesses. Then, we'll discuss some basic concepts that we'll need in order to write our first program.

# ## History of C

The C language was developed at Bell Labs in the early 1970s by Dennis Ritchie and others. At that time, the *Unix* operating system, also developed at Bell Labs, was written in assembly language. Programs written in assembly are usually hard to debug, maintain, and enhance, and *Unix* was no exception. Ritchie decided to rewrite *Unix* code in another language that would make the execution of these tasks easier. He named the language C because it was the evolution of an earlier language written by Ken Thompson, called B. The C language continued to evolve during the 1970s, and since then, it has been used by thousands of programmers for a wide variety of applications.

# ## The ANSI Standard

The rapid expansion of the C language and its increased popularity led many companies to develop their own C compilers. Due to the absence of an official standard, their development relied on the bible of C programmers, the legendary K&R book, written by Brian Kernighan and Dennis Ritchie in 1978.

However, the K&R book was not written in the precise way that a standard requires. Features that were not clearly described could be implemented in different ways. As a result, the same program could be compiled with one C compiler and not with another. In parallel, the C language continued to evolve with the addition of new features and the replacement or obsolescence of existing ones.

The need for the standardization of C language became apparent. In 1983, the American National Standard Institute (ANSI) began the development of the C standard that was completed and formally approved, in 1989, as ANSI C or Standard C. In 1990, the ANSI C standard was adopted by the International Standards Organization (ISO) as ISO/IEC 9899:1990. This standard describes precisely the features, characteristics, and properties of the C language, and every C compiler must support it.

The addition of some new features to the ANSI standard during the late 1990s led to a new standard called C99. C99 was further enriched with new features, leading to the publication of the C11 standard. This book describes the C language based on the ANSI/ISO C standard.