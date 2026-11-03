# 11.10 String I/O

# 11.10.1 fputs()

Declaration: int fputs(const char *str, FILE *fptr);

This function writes the null terminated string pointed to by str to a file. The null character that mark the end of string is not written to the file. On success it returns the last character written and on error it returns EOF.

```
/*P11.5 Program to understand the use of fputs()*/
#include<stdio.h>
main()
{
FILE *fptr;
char str[80];
fptr=fopen("test.txt","w");
printf("Enter the text\n");
printf("To stop entering, press Ctrl+d in Unix and Ctrl+z in Dos\n");
while(gets(str)!=NULL)
fputs(str,fptr);
fclose(fptr);
}
```

Suppose we enter this text after running the program-

Yesterday is history
Tomorrow is mystery
Today is a gift
That's why it is called Present
^Z

When the first line of text is entered and Enter key is pressed, the function gets() converts the newline character to the null character and the array str contains "Yesterday is history"( 20 characters +1 null character). Now str is written to the file test.txt using fputs(). The null character is not written the file, so only 20 characters are written.

In previous chapters we had studied about the function puts() that prints the string on the screen. The difference between these two functions is that puts() translates null character to a newline, but fputs() does not. fputs() will write a newline character to the file only if it is contained in the string. So after the first line of text newline character is not entered in the file. Immediately after the first line of text, the second one is written. In the next program we'll see how to read this file using fgets()

# 11.10.2 fgets()

Declaration: char *fgets(char *str, int n, FILE *fptr);

This function is used to read characters from a file and these characters are stored in the string point to by str. It reads at most n-1 characters from the file where n is the second argument. fptr is a file pointer which points to the file from which characters are read. This function returns the string point to by str on success, and on error or end of file it returns NULL.