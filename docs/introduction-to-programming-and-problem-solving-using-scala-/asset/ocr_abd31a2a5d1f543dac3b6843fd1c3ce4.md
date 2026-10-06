# # Chapter 9

# ## Text Files

+   9.1 I/O Redirection ................................................................................ 234
9.2 Packages and import Statements ............................................................ 234
9.3 Reading from Files ..................................................................................... 236
    9.3.1 FileNotFoundException and IOException ............................................... 236
    9.3.2 Iterators ....................................................................................... 237
    9.3.3 String split Method ........................................................................ 239
    9.3.4 Reading from Other Things ................................................................ 240
    9.3.5 Other Options (Java Based) ......................................................... 241
9.4 Writing to File ...................................................................................... 242
    9.4.1 Appending to File ......................................................................... 242
        printf and format ................................................................................... 243
9.5 Use Case: Simple Encryption ................................................................... 244
    9.5.1 Command Line Arguments ................................................................ 244
    9.5.2 Mapping a File ............................................................................ 245
    9.5.3 Character Offset ........................................................................ 245
    9.5.4 Alphabet Flip ............................................................................ 246
    9.5.5 Key Word ................................................................................... 246
    9.5.6 Putting It Together ........................................................................ 247
    9.5.7 Primes and Real Cryptography ...................................................... 248
9.6 End of Chapter Material .................................................................... 249
    9.6.1 Summary of Contents ................................................................ 249
    9.6.2 Self-Directed Study ................................................................... 250
    9.6.3 Exercises ................................................................................... 250
    9.6.4 Projects ..................................................................................... 251

Most of the programs that you use on a regular basis would be far less useful if they did not have the ability to read from and write to files. Consider a word processor that could not save your files and let you load them back in later. A program where you had to print output to paper before you closed the program to have any record of what you had done. Such a program would not be very useful, and it would not be used much. That is true even if provided you with a very full set of other capabilities.

The reason for this is that all the work you do without a file sits in the temporary memory of the computer that is given to the application when it runs. When the application is stopped, for any reason, all of memory is lost. It might be given over to other applications or used by the operating system. Whatever happens to it, you no longer have the ability to get it in any useful way.

Files give you the ability to store values from one run of a program to the next. Files can also be used to store information that you do not want to have to write into the source code or just to store amounts of information larger than what will fit in the memory of the machine. Disk drives are much slower than memory so this last part has to be done with a level of care.