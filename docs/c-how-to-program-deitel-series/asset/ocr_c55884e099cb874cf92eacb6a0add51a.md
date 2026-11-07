```
```cpp
// output summary of results
cout << "\nNumber of students who received each letter grade:"
     << "\nA: " << aCount // display number of A grades
     << "\nB: " << bCount // display number of B grades
     << "\nC: " << cCount // display number of C grades
     << "\nD: " << dCount // display number of D grades
     << "\nF: " << fCount // display number of F grades
     << endl;
} // end function displayGradeReport
```
```

**Fig. 5.10 |** GradeBook class uses switch statement to count letter grades. (Part 3 of 3.)

# Reading Character Input

The user enters letter grades for a course in member function inputGrades (lines 49–98). In the while header, in line 57, the parenthesized assignment (grade = cin.get()) executes first. The cin.get() function reads one character from the keyboard and stores that character in integer variable grade (declared in line 51). Normally, characters are stored in variables of type char; however, characters can be stored in any integer data type, because types short, int, long and long long are guaranteed to be at least as big as type char. Thus, we can treat a character either as an integer or as a character, depending on its use. For example, the statement

```
```cpp
cout << "The character " << 'a' << " has the value "
     << static_cast<int> ( 'a' ) << endl;
```
```

prints the character and its integer value as follows:

```
```text
The character (a) has the value 97
```
```

The integer 97 is the character’s numerical representation in the computer. Appendix B shows the characters and decimal equivalents from the ASCII (American Standard Code for Information Interchange) character set.

Generally, assignment statements have the value that’s assigned to the variable on the left side of the =. Thus, the value of the assignment expression grade = cin.get() is the same as the value returned by cin.get() and assigned to the variable grade.

The fact that assignment expressions have values can be useful for assigning the same value to several variables. For example,

```
```cpp
a = b = c = 0;
```
```

first evaluates c = 0 (because the = operator associates from right to left). The variable b is then assigned the value of c = 0 (which is 0). Then, a is assigned the value of b = (c = 0) (which is also 0). In the program, the value of grade = cin.get() is compared with the value of EOF (a symbol whose acronym stands for “end-of-file”). We use EOF (which normally has the value −1) as the sentinel value. However, you do not type the value −1, nor do you type the letters EOF as the sentinel value. Rather, you type a system-dependent keystroke combination that means “end-of-file” to indicate that you have no more data to enter. EOF is symbolic integer constant that is included into the program via the <iostream> header.¹ If the value assigned

1. To compile this program, some compilers require the header <cstdio> which defines EOF.