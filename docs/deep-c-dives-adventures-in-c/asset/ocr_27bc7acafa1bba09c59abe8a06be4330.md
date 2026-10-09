character code in hex and press ENTER when finished. As you type the character code you will see the hex displayed and you only see the Unicode character after you press ENTER.
For example:

```
```
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char **argv)
{
  printf("Sum Sigma %s\n", "Σ");
}
```
```

The sigma is typed in under Linux using CTRL+SHIFT+u 2211 ENTER and under Windows it is better to copy and paste it. If you run the program you will see:
Sum Sigma Σ
Under Windows you will need to change the code page of the terminal window by using; chcp 65001
to set the UTF-8 code page.

What is important here is not so much that Unicode with UTF-8 sort of works, it is the idea that UTF-8 is just another sequence of bit patterns. A C string is a sequence of bytes where usually each byte is the code for an ASCII character, but in most cases the functions that work with strings don't care what the bytes represent – they simply manipulate the bytes.
For example:

```
```
char myString[] = "Σ";
  printf("%s\n", myString);
  printf("%d\n", strlen(myString));
  char myString2[100] = "Sum Sigma ";
  strcat(myString2, myString);
  printf("%s\n", myString2);
```
```

It looks as if we have set myString to a single character, but this ignores the fact that as a UTF-8 encoding it needs the three bytes 0xE2, 0x88 and 0x91. The string displays perfectly as long as it is sent to a destination that accepts UTF-8 encoded data. The Linux terminal used with VS Code does, but the Windows terminal has to be set to UTF-8 mode by selecting a code page. The C program still knows nothing about UTF-8; it just sends the contents of the three-character string to the terminal for display. The next instruction displays the length of the string and it is indeed 3 and not 1. Next we concatenate two strings. Again the strcat function doesn't care that myString is UTF-8 encoded. As far as it is concerned it contains three