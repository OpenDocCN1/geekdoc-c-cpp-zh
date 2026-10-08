# APPENDIX F Classes and Objects

section.) The Salesperson employee; statement in Line 26 uses the Salesperson class definition to instantiate a Salesperson object employee. The employee object contains three data members: a string variable name and two double named sales and bonus. As the program in Figure-4 shows you use employee., to refer to the name in the employee object. You use employee. sales and bonus employee. to refer to the employee object's sales and bonus vari-. Figure-5 shows a sample run of the Sweets Unlimited program, and Figure F-6 shows the contents of the salesinfo.txt file created by the program.

![](bbox=[0.316, 0.25, 0.854, 0.47])

Figure-5 Sample run of the Sweets Unlimited program

![](bbox=[0.316, 0.533, 0.604, 0.653])

Figure-6 Contents of the salesinfo.txt file displayed in a text editor

# Header Files

Although you can enter a class definition in the program that you enter a class definition in a separate file called a header file. As shown earlier in Figure-4, most programmers use a header file. Figure-7 shows the definition of the Salesperson class header entered in a .cpp file. Unlike program files, which end with .cpp, header filenames end with .h. You will learn how to add a header file to a solution in F-2, which is contained in the Cpp6_Appendix.pdf file. Figure-8 shows a modified version of the Sweets Unlimited program. Unlike the original program, the modified program does not contain the Salesperson class definition. Instead, the modified program uses the class definition contained in the Salesperson.h header file. Typically, a header file is stored in the same location as the program