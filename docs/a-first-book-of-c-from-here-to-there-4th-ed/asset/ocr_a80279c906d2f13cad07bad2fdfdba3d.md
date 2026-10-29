# Strings as Character Arrays

2. (Program) a. The following function, convert(), “marches along” the C-string passed to it and sends each character in the string one at a time to the ToUpper() function until the NULL character is encountered:

```
```cpp
// convert a string to uppercase letters
void convert(char strng[])
{
    int i = 0;
    while (strng[i] != '\0')
    {
        strng[i] = ToUpper(strng[i]);
        i++;
    }

    return;
}

char ToUpper(char letter) // convert a character to uppercase
{
    if( letter >= 'a' && (letter <= 'z') )
        return (letter - 'a' + 'A');
    else
        return (letter);
}
```
```

The ToUpper() function takes each character passed to it and examines it to determine whether the character is a lowercase letter (any character from a to z). Assuming that characters are stored with the standard ASCII character codes, the expression letter - 'a' + 'A' converts a lowercase letter to its uppercase equivalent. Rewrite the convert() function with pointers.

b. Include the convert() and ToUpper() functions in a working program. The program should prompt the user for a string and display the string in uppercase letters.

+   3. (Program) Using pointers, repeat Exercise 1 from Section 15.1.
+   
+   4. (Program) Using pointers, repeat Exercise 2 from Section 15.1.
+   
+   5. (Program) Using pointers, repeat Exercise 3 from Section 15.1.
+   
+   6. (Program) Write a function named remove() that returns nothing and deletes all occurrences of a character from a C-string. The function should take two arguments: the string name and the character to remove. For example, if the message contains the string Happy Holidays, the function call remove(message, 'H') should place the string appy olidays in message.
+   
+   7. (Program) Using pointers, repeat Exercise 6 from Section 15.1.
+   
+   8. (Program) Write a program using the cin.get() and toupper() library functions, along with a cout stream object to display each entered letter in its uppercase form. The program should terminate when the 1 key (the digit) is pressed.