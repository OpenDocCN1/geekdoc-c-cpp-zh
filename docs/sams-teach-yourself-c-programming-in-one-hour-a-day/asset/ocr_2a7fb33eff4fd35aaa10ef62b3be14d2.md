c. "+12hundred"

f. "negative100"

+   3. What would the atof() function return if passed the following?

+   a. "65"

+   b. "81.23"

+   c. "-34.2"

+   d. "ten"

+   e. "+12hundred"

+   f. "1e+3"

+   4. BUG BUSTER: Is anything wrong with the following?

```
char *string1, string2;
string1 = "Hello World";
strcpy(string2, string1);
printf("%s %%s", string1, string2);
```

Because of the many possible solutions, answers aren't provided for the following exercises.

+   5. Write a program that prompts for the user's last name, first name, and middle name individually. Store the name in a new string as first initial, space, middle initial, period, space, and last name. For example, if Ruth, Claire, and Alber are entered, store R. C. Alber. Display the new name to the screen.

+   6. Write a program to prove your answers to questions 8 and 9.

+   7. The function strstr() finds the first occurrence of one string within another, and it is case-sensitive. Write a function that performs the same task without case-sensitivity.

+   8. Write a function that determines the number of times one string occurs within another.

+   9. Write a program that searches a text file for occurrences of a user-specified target string and reports the line numbers where the target is found. For example, if you search one of your C source files for the string "printf()", the program should list all the lines where the printf() function is called by the program.

+   10. Listing 18.13 demonstrates a function that inputs an integer from stdin. Write a function get_float() that inputs a floating-point value from stdin.