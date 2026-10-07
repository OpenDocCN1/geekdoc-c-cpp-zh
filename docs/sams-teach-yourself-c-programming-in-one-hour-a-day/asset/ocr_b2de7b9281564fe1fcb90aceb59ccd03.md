# LESSON 10 Working with Characters Strings

pointer to the string that you want displayed. The printf() function displays the string onscreen, stopping when it reaches the string's terminating null character, for example:

```
char *str = "A message to display";
printf("%s", str);
```

You can also display multiple strings and mix them with literal text and/or numeric variables:

```
char *bank = "First Federal";
char *name = "John Doe";
int balance = 1000;
printf("The balance at %s for %s is %d.", bank, name, balance);
```

The resulting output is

The balance at First Federal for John Doe is 1000.

For now, this information should be sufficient for you to display string data in your programs. Complete details on using printf() are given in Lesson 14, "Working with the Screen, Printer, Keyboard."

# Reading Strings from the Keyboard

In addition to displaying strings, programs often need to accept inputted string data from the user via the keyboard. The C library has two functions that can be used for this purpose: gets() and scanf(). Before you can read a string from the keyboard, however, you must have where to put it. You can create space for string storage using either of the methods discussed earlier—an array declaration or the malloc() function.

# Inputting Strings Using the gets() Function

The gets() function gets a string from the keyboard. When gets() is called, it reads all characters typed at the keyboard up to the first newline character (which you generate by pressing Enter). This function discards the newline, adds a null character, and gives the string to the calling program. The string is stored at the location indicated by a pointer to type char passed to gets(). A program that uses gets() must include the file stdio.h. Listing 10.5 presents an example.