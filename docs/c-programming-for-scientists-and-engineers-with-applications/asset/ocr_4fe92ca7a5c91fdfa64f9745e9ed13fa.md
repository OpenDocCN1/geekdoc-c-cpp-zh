Use of scanf() and printf() Functions Character data may be entered from a keyboard or may be read from a data file using the scanf() or fscanf() functions, respectively.

When character data is input using the scanf() function the control field is "%nc", where n is the number of characters. The following code shows the input of a character array from the keyboard. When reading the input characters, scanf() ignores any leading blanks and starts reading with the first nonblank character. The scanf() function reads the input characters including embedded and trailing blanks until the required number of characters have been read. The following sample code shows the input and output of character arrays.

```
#include <stdio.h>

int main() {
    char name[20];
    printf("Enter the name:\n");
    scanf("%15c\n", name);
    printf("The name entered is: %%15c\n", name);

    return 0;
}
```

The input and output of this code is as follows:

Enter the name: JOHNNY APPLESEED
The name entered is: JOHNNY APPLESEE

In the input statement there is no need to specify the address operator "&" in front of the char array name, because name is the address of the array. Notice that 15 characters are read, which may include the new line feed '\n' or trailing blanks. Since 15 characters have been specified, 15 characters will be read including embedded or trailing blanks and control characters. If more than 15 characters are entered, only 15 characters are read because of the specification %15c in the control field. Thus, the rest of the characters entered are ignored. Since 16 characters are entered, the character "D" is ignored.

The characters are stored as follows:

| J O H N N Y A P P L E S E E | | | | | | |
| 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 |