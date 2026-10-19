
## Metrics Reporters

> **Cross-Reference** For more information on metrics, see Section 28.4, “Measurement.”

Some tools analyze your code and report on its quality. For example, you can obtain tools that report on the complexity of each routine so that you can target the most complicated routines for extra review, testing, or redesign. Some tools count lines of code, data declarations, comments, and blank lines in either entire programs or individual routines. They track defects and associate them with the programmers who made them, the changes that correct them, and the programmers who make the corrections. They count modifications to the software and note the routines that are modified the most often. Complexity analysis tools have been found to have about a 20 percent positive impact on maintenance productivity (Jones 2000).

## Refactoring Source Code

A few tools aid in converting source code from one format to another.

### Refactorers

> **Cross-Reference** For more on refactoring, see Chapter 24, “Refactoring.”

A refactoring program supports common code refactorings either on a standalone basis or integrated into an IDE. Refactoring browsers allow you to change the name of a class across an entire code base easily. They allow you to extract a routine simply by highlighting the code you’d like to turn into a new routine, entering the new routine’s name, and ordering parameters in a parameter list. Refactorers make code changes quicker and less error-prone. They’re available for Java and Smalltalk and are becoming available for other languages. For more about refactoring tools, see Chapter 14, “Refactoring Tools” in *Refactoring* (Fowler 1999).

### Restructurers

A restructurer will convert a plate of spaghetti code with gotos to a more nutritious entrée of better-structured code without gotos. Capers Jones reports that in maintenance environments code restructuring tools can have a 25–30 percent positive impact on maintenance productivity (Jones 2000). A restructurer has to make a lot of assumptions when it converts code, and if the logic is terrible in the original, it will still be terrible in the converted version. If you’re doing a conversion manually, however, you can use a restructurer for the general case and hand-tune the hard cases. Alternatively, you can run the code through the restructurer and use it for inspiration for the hand conversion.

### Code Translators

Some tools translate code from one language to another. A translator is useful when you have a large code base that you’re moving to another environment. The hazard in using a language translator is that if you start with bad code the translator simply translates the bad code into an unfamiliar language.

## Version Control

> **Cross-Reference** These tools and their benefits are described in “Software Code Changes” in Section 28.2.

You can deal with proliferating software versions by using version-control tools for

- Source-code control
- Dependency control like that offered by the make utility associated with UNIX
- Project documentation versioning
- Relating project artifacts like requirements, code, and test cases so that when a requirement changes, you can find the code and tests that are affected

## Data Dictionaries

A data dictionary is a database that describes all the significant data in a project. In many cases, the data dictionary focuses primarily on database schemas. On large projects, a data dictionary is also useful for keeping track of the hundreds or thousands of class definitions. On large team projects, it’s useful for avoiding naming clashes. A clash might be a direct, syntactic clash, in which the same name is used twice, or it might be a more subtle clash (or gap) in which different names are used to mean the same thing or the same name is used to mean subtly different things. For each data item (database table or class), the data dictionary contains the item’s name and description. The dictionary might also contain notes about how the item is used.

250 files or recompiling each file manually, forgetting one, and getting weird out-of-synch errors. Overall, build tools like make or ant substantially improve the time and reliability of the average compile-link-run cycle.

Some groups have found interesting alternatives to dependency-checking tools like make. For example, the Microsoft Word group found that simply rebuilding all source files was faster than performing extensive dependency checking with make as long as the source files themselves were optimized (header file contents and so on). With this approach, the average developer’s machine on the Word project could rebuild the entire Word executable—several million lines of code—in about 13 minutes.

## Code Libraries

A good way to write high-quality code in a short amount of time is not to write it all but to find an open source version or buy it instead. You can find high-quality libraries in at least these areas:

- Container classes
- Credit card transaction services (e-commerce services)
- Cross-platform development tools. You might write code that executes in Microsoft Windows, Apple Macintosh, and the X Window System just by recompiling for each environment.
- Data compression tools
- Data types and algorithms
- Database operations and data-file manipulation tools
- Diagramming, graphing, and charting tools
- Imaging tools
- License managers
- Mathematical operations
- Networking and internet communications tools
- Report generators and report query builders
- Security and encryption tools
- Spreadsheet and grid tools
- Text and spelling tools
- Voice, phone, and fax tools

## Code Tuning

These tools can help you fine-tune your code.

### Execution Profilers

An execution profiler watches your code while it runs and tells you how many times each statement is executed or how much time the program spends on each statement or execution path. Profiling your code while it’s running is like having a doctor press a stethoscope to your chest and tell you to cough. It gives you insight into how your program works, where the hot spots are, and where you should focus your code-tuning efforts.

### Assembler Listings and Disassemblers

Some day you might want to look at the assembler code generated by your high-level language. Some high-level-language compilers generate assembler listings. Others don’t, and you have to use a disassembler to re-create the assembler from the machine code that the compiler generates. Looking at the assembler code generated by your compiler shows you how efficiently your compiler translates high-level-language code into machine code. It can tell you why high-level code that looks fast runs slowly. In Chapter 26, “Code-Tuning Techniques,” several of the benchmark results are counter-intuitive. While benchmarking that code, I frequently referred to the assembler listings to better understand the results that didn’t make sense in the high-level language.

If you’re not comfortable with assembly language and you want an introduction, you won’t find a better one than comparing each high-level-language statement you write to the assembler instructions generated by the compiler. A first exposure to assembler is often a loss of innocence. When you see how much code the compiler creates—how much more than it needs to—you’ll never look at your compiler in quite the same way again.

Conversely, in some environments the compiler must generate extremely complex code. Studying the compiler output can foster an appreciation for just how much work would be required to program in a lower level language.

## 30.4 Tool-Oriented Environments

Some environments have proven to be better suited to tool-oriented programming than others.

The UNIX environment is famous for its collection of small tools with funny names that work well together: grep, diff, sort, make, crypt, tar, lint, ctags, sed, awk, vi, and others. The C and C++ languages, closely coupled with UNIX, embody the same philosophy; the standard C++ library is composed of small functions that can easily be composed into larger functions because they work so well together.
