
## Part 1: Programming Fundamentals Quickstart

Whether you're a student getting a sense of the textbook you'll be using, an instructor planning your course syllabus or a professional software developer deciding which chapters to read as you prepare for a project, the following chapter overviews will help you make the best decisions.

Chapter 1, Introduction to Computers and C, engages novice students with intriguing facts and figures to excite them about studying computers and computer programming. The chapter includes current technology trends, hardware and software concepts and the data hierarchy from bits to databases. It lays the groundwork for the C programming discussions in Chapters 2–15, the appendices and the integrated case studies.

We discuss the programming-language types and various technologies you're likely to use as we develop software. We introduce the C standard library—existing, reusable, top-quality, high-performance functions to help you avoid “reinventing the wheel.” You'll enhance your productivity by using libraries to perform significant tasks while writing only modest numbers of instructions. We also introduce the Internet, the World Wide Web, the “Cloud” and the Internet of Things (IoT), laying the groundwork for modern applications development.

This chapter's test-drives demonstrate how to compile and execute C code with

- Microsoft's Visual C++ in Visual Studio on Windows,
- Apple's Xcode on macOS, and
- GNU's gcc on Linux.

We've run the book's 147 code examples using each environment. Choose whichever program-development environment you prefer—the book works well with others, too.

We also demonstrate GNU gcc in the GNU Compiler Collection Docker container. This enables you to run the latest GNU gcc compiler on Windows, macOS or Linux—this is important because the GNU compilers generally implement all (or most) features in the latest language standards. See the Before You Begin section that follows this Preface for compiler installation instructions. See the Docker section later in this Preface for more information on this important developer tool. For Windows users, we point to Microsoft's step-by-step instructions that allow you to install Linux in Windows via the Windows Subsystem for Linux (WSL). This is another way to be able to use the GNU gcc compiler on Windows.

You'll learn just how big “big data” is and how quickly it's getting even bigger. The chapter closes with an introduction to artificial intelligence (AI)—a key overlap between the computer-science and data-science fields. AI and data science are likely to play significant roles in your computing career.

Chapter 2, Intro to C Programming, presents C fundamentals and illustrates key language features, including input, output, fundamental data types, computer memory concepts, arithmetic operators and their precedence, and decision making.

**Chapter 3, Structured Program Development**, is one of the most important chapters for programming novices. It focuses on **problem-solving and algorithm development** with C’s **control statements**. You’ll **develop algorithms through top-down, stepwise refinement**, using the if and if…else selection statements, the while iteration statement for counter-controlled and sentinel-controlled iteration, and the increment, decrement and assignment operators. The chapter presents three algorithm-development case studies.

**Chapter 4, Program Control**, presents C’s other **control statements**—for, do…while, switch, break and continue—and the logical operators. A key feature of this chapter is its **structured-programming summary**.

**Chapter 5, Functions**, introduces program construction using existing and custom functions as building blocks. We demonstrate **simulation techniques** with **random-number generation**. We also discuss passing information between functions and how the function-call stack and stack frames support the function call/return mechanism. We begin our treatment of recursion. This chapter also presents our first simulation case study—**Building a Casino Game**, which is enhanced by end-of-chapter exercises.

## Part 2: Arrays, Pointers and Strings

**Chapter 6, Arrays**, presents C’s built-in **array data structure** for representing lists and tables of values. You’ll define and initialize arrays, and refer to their individual elements. We discuss passing arrays to functions, sorting and searching arrays, manipulating multidimensional arrays and creating variable-length arrays whose size is determined at execution time. **Chapter 13, Computer-Science Thinking: Sorting Algorithms and Big O**, discusses more sophisticated and higher-performance sorting algorithms and presents a friendly introduction to **analysis of algorithms** with computer science’s **Big O** notation. Chapter 6 presents our first data-science case study—**Intro to Data Science: Survey Data Analysis**. In the exercises, we also present two **Game Programming with Graphics, Sound and Collision Detection** case studies and an **Embedded Systems Programming** case study (**Robotics with the Webots Simulator**).

**Chapter 7, Pointers**, presents what is arguably C’s most powerful feature. Pointers enable programs to

- accomplish pass-by-reference,
- pass functions to other functions, and
- create and manipulate dynamic data structures, which you’ll study in detail in Chapter 12.

The chapter explains pointer concepts, such as declaring pointers, initializing pointers, getting the memory address of a variable, dereferencing pointers, pointer arithmetic and the close relationship between arrays and pointers. This chapter presents our first systems software case-study exercise—**Building Your Own Computer with Simulation**. This case study introduces an essential modern computer-architecture topic—**virtual machines**.

Chapter 8, Characters and Strings, introduces the C standard library’s string, character and memory-block processing functions. You’ll use these powerful capabilities in Chapter 11, File Processing, as you work through a natural language processing (NLP) case study. You’ll see that strings are intimately related to pointers and arrays.

## Part 3: Formatted Input/Output, Structures and File Processing

Chapter 9, Formatted Input/Output, discusses the powerful formatting features of functions scanf and printf. When properly used, these functions securely input data from the standard input stream and output data to the standard output stream, respectively.

Chapter 10, Structures, Unions, Bit Manipulation and Enumerations, introduces structures (structs) for aggregating related data items into custom types, unions for sharing memory among multiple variables, typedefs for creating aliases for previously defined data types, bitwise operators for manipulating the individual bits of integral operands and enumerations for defining sets of named integer constants. Many C programmers go on to study C++ and object-oriented programming. In C++, C’s structs evolve into classes, which are the "blueprints" C++ programmers use to create objects. C structs contain only data. C++ classes can contain data and functions.

Chapter 11, File Processing, introduces files for long-term data retention, even when the computer is powered off. Such data is said to be "persistent." The chapter explains how plain-text files and binary files are created, updated and processed. We consider both sequential-access and random-access file processing. In one of our case-study exercises, you’ll read data from a comma-separated value (CSV) file. CSV is one of the most popular file formats in the data-science community. This chapter presents our next case study—Building a Random-Access Transaction-Processing System. We use random-access files to simulate the kind of high-speed direct-access capabilities that industrial-strength database-management systems have. This chapter also presents our first artificial-intelligence/data-science case study, which uses Natural Language Processing (NLP) techniques to begin investigating the controversial question, "Who really wrote the works of William Shakespeare?" A second artificial-intelligence/data-science case study—Machine Learning with the GNU Scientific Library—investigates Anscombe’s Quartet using simple linear regression. This is a collection of four dramatically different datasets that have identical or nearly identical basic descriptive statistics. It offers a valuable insight for students and developers learning some data-science basics in this computer-science textbook. The case study then asks you to run a simple linear regression on 126 years of New York City average January temperature data to determine if there is a cooling or warming trend.
