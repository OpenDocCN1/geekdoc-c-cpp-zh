# Analysis ▼

This program compares two strings defined on lines 6 and 7. Lines 13 and 14 print the strings to the screen that the user can see what they are. The program executes while loop on lines 16-27 so that multiple compares can be done. If the user asks to compare zero characters on lines 18 and 19, the program breaks on line 22; otherwise, the strncmp executes on line 24, and the result is printed on line 26.

# Searching Strings

The C library contains a number of functions that search strings. To put it another way, these functions determine whether one string occurs within another string, and so, where. you can choose from six string searching functions, all of which require the header file string.h:

+   - strchr()
- strchr()
- strcspn()
- strspn()
- strpbrk()
- strstr()

# The strchr() Function

The strchr() function finds the first occurrence of a specified character in a string. The prototype is

```
char *strchr(const char *str, int ch);
```

The function strchr() searches string from left to right until the character ch is found or the terminating null character is found. If ch is found, a pointer to it is returned. If not, NULL is returned.

When strchr() finds the character, it returns a pointer to that. Knowing that str is a pointer to the first character in the string, you can obtain the position of the found character by subtracting str from the pointer returned by strchr(). Listing that the first character in a string is at position 0. Like many of C's string functions, strchr() is case-sensitive and, therefore, reports that the character "F" isn't found in the string "raffle".