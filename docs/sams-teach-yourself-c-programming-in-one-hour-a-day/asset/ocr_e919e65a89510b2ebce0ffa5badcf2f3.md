5. Because p is a type void pointer, it must be cast to the proper type before being
used in an assignment statement. The third line should be as follows:

*(float)p = 1.23.

+   6. No When using fields, you must place them within a structure first. The following is correct:
```c
struct quiz_answers
{
  unsigned answer1 : 1;
  unsigned answer2 : 1;
  unsigned answer3 : 1;
  unsigned answer4 : 1;
  unsigned answer5 : 1;
  char student_name[15];
-Dean}
```

# Answers for Lesson 22

# Quiz

+   1. Modular programming refers to the program development method that breaks a
program into multiple source-code files.
2. The main module contains the main() function.
3. To avoid unwanted side effects by ensuring that complex expressions passed as
arguments to the macro are fully evaluated.
4. Compared to a function, a macro results in faster program execution but larger gram size.
5. The defined() operator tests to see whether a particular name is defined, returning
TRUE if the name is defined and FALSE if it isn't.
6. You must use #endif.
7. Compiled source files become object files with an .OBJ extension.
8. #include copies the contents of another file into the current file.
9. An #include statement with double quotes includes into the current directory for the
include file. An include statement with <> searches the standard directory for the
include file.
10. __DATE__ is used to place into the program the date that the program was
compiled.
11. A string containing the name of the current program, including path information.