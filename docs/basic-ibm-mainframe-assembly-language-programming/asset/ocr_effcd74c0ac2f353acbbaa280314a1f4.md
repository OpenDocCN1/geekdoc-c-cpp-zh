# 5. Hello World

# 5.1 The z390 Portable Mainframe Project

The examples in this book were developed using the z390 Portable Mainframe Assembler and Emulator. This is a Java based, GPL licensed project to "...Enable z390 and zcobol users to compile, assemble, link, and execute mainframe COBOL and assembler problem state programs with minimum source code changes using Windows, Linux, and other platforms supporting the J2SE runtime...." from the web site:

http://www.z390.org/

The emulator can be run either in a graphical user window or from a command prompt.

# 5.2 Hello World

Now it's time to write the customary Hello World program as shown in Figure 1.

The first few lines of every assembly program deal with assembler directives and linkage. Linkage refers to the process of connecting your program to the program that called it. It involves saving the calling program's registers so they can be restored at exit, establishing a base register for your program, and creating a save area in your program. These will each be discussed later in this book. Normally these actions are done with macros (macros are small, pre-written, disk resident, code modules) as they seldom differ from one program to the next.

The z390 emulator has a macro named SUBENTRY that establishes your program's linkage, its save area, and sets register 13 as your base register.

When you assemble a program, the assembler will generate a file showing your program and its translation to machine language along with other information. This is often referred to as the listing and, in the z390 emulator, will appear as a file with the same name as your program but with the .PRN file extension.

The directive PRINT NOGEN is a directive to the assembler that tells it to display the names of the macros but not show the macro expansion (code) itself in the listing. If PRINT NOGEN is omitted, the assembler will display the contents of the of the macro expansion which are usually not very interesting after you see them once.

The label on SUBENTRY is HELLO. The SUBENTRY macro uses this label to establish the external linkage name of your program. This is the name other programs would use if they were calling