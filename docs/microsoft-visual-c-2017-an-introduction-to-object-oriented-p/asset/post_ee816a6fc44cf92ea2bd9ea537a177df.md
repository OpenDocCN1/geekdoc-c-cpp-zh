
# Acknowledgments

Thank you to all of the people who make this book a success, including Alyssa Pratt, Senior Content Developer; and Jennifer Feltri-George, Content Project Manager. I want to acknowledge every Cengage Learning Consultant who travels the country guiding instructors in their choices of educational materials.

Thanks, too, to my husband, Geoff, for his constant support and encouragement. Finally, the book is dedicated to the newest member of our family arriving in June, 2017, after this book goes to print. We don't yet know your first name, Baby Farrell-Peterson, but I am excited and filled with love awaiting the arrival.

Joyce Farrell

# Read This Before You Begin

### To the User of the Data Files

To complete the steps and projects in this book, you need data files that have been created specifically for this book. Your instructor will provide the data files to you. You can also obtain the files electronically from CengageBrain. Find the ISBN of your title on the back cover of your book, enter the ISBN in the search box at the top of the CengageBrain home page. You can find the data files on the product page that opens. Note that you can use a computer in your school lab or your own computer to complete the exercises in this book.

### Using Your Own Computer

To use your own computer to complete the steps and exercises, you will need the following:

- Software—Microsoft Visual C# 2017, including the Microsoft .NET Framework.
- Hardware—Minimum requirements identified by Microsoft are a 1.8 GHz CPU, 2 GB of RAM, 1GB to 40GB of hard disk space, depending on features installed, and a display with resolution of 1280 by 720.
- Operating system—Windows 10, or with updates, 7 or 8.

# CHAPTER 1 A First Program Using C#

Upon completion of this chapter, you will be able to:

- Describe the programming process
- Differentiate between procedural and object-oriented programming
- Describe the features of object-oriented programming languages
- Describe the C# programming language
- Write a C# program that produces output
- Select identifiers to use within your programs
- Improve programs by adding comments and using the System namespace
- Compile and execute a C# program using the command prompt and using Visual Studio

Programming a computer is an interesting, challenging, fun, and sometimes frustrating task. As you learn a programming language, you must be precise and careful as well as creative. Computer programmers must learn to plan a program's logic, and choose from a variety of programming languages, such as Visual Basic, Java, and C++, in to implement their logic. C# (pronounced "C Sharp") is a relatively-new programming language that offers a wide range of options and features. As you work through this book, you will master many of them, one step at a time. If this is your first programming experience, you will learn new ways to approach and solve problems and think logically. If you know how to program but are not C#, you will be impressed by its capabilities.

In this chapter, you will learn the background of programming that led to the development of C#, and you will write and execute your first C# programs.

## The Programming Process

A computer program is a set of instructions that tells a computer what to do. Programs are also software; software operates in two broad categories:

- System software describes the programs that operate the computer. Examples include operating systems such as Microsoft Windows, Mac OSX, and Linux.
- Application software describes the programs that allow users to complete tasks such as creating documents, calculating paychecks, and playing games. (Application software programs are often called apps.)

The physical devices that make up a computer are called hardware. Internally, computer hardware is constructed from circuitry that consists of on/off switches; the most basic circuit-level language computers use to control the operation of switches is called machine language. Machine language is expressed as a series of Is and Os represent switches that are on, and Os represent switches that are off. If programmers had to write computer programs using machine language, and Is and Os involved in programming any worthwhile task, the hundreds of thousands of Is would be a time-consuming and difficult task, but modifying programs, understanding others' programs, and locating errors within all programs could be cumbersome. Additionally, the number and location of switches vary from computer to computer, which means you would need to customize a machine-language program for every type of machine on which the program had to run.

Fortunately, programming has become easier because of the development of high-level programming languages. A high-level programming language allows you to use a limited vocabulary of reasonable keywords. Keywords are predefined and reserved identifiers that have special meaning in a language. High-level languages contain keywords such as read, write, and add that you use instead of the sequence of on/off switches perform these tasks. High-level languages also allow you to assign names to areas of computer memory; you can use names without spaces, such as hoursWorked or payRate, rather than having to remember the memory locations (switches) of many values.

Camel casing, or lower casing, describes the style of identifiers such as hoursWorked and appear to have a hump in the middle because they start with a lowercase letter but contain uppercase letters to identify new words. By convention in C#, data items use camel casing. The C# programming language is sensitive. Therefore, if you create an identifier payRate, you cannot refer to it later using identifiers as PayRate or payrate.

Each high-level language has its syntax, or rules of the language. For example, to produce output, you might use the verb print in one language and write in another. All languages have a specific, limited vocabulary with a set of rules for using that vocabulary. Programmers use a computer program called a compiler to translate their high-level language statements into machine code. The compiler issues an error message each time the programmer commits a syntax error—that is, the programmer can correct the error and attempt another translation by compiling the program again. The program can be completely translated to machine language only when all syntax errors have been corrected. When you learn a computer language such as C#, C++, Visual Basic, or Java, you must learn both the vocabulary and syntax rules for that language.

In many languages, such as BASIC, the language translator is called an interpreter. In others, such as assembly language, it is called an assembler. The various language translators operate differently, but the ultimate goal of each is to translate the higher-level language into machine language.

In learning the correct syntax for a particular language, a programmer must understand computer programming logic. The logic behind any program involves executing the various statements and procedures in the correct order to produce the desired results. For example, you might have to execute perfect individuals on a musical instrument, but if you do not execute them in the proper order (execute a B-flat when an F-sharp was expected), no one will enjoy your performance. Similarly, you might be able to use a computer language's syntax correctly but be unable to obtain correct results because the program is not constructed logically. Examples of logical errors include multiplying two values when you should divide them, or attempting to calculate a paycheck before obtaining the appropriate payroll data.
