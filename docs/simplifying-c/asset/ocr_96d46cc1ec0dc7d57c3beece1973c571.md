```
```c
/* Reading characters from a file*/
while ((c_temp=fgetc(fp_names))!=EOF)
{
/* Displaying characters in screen*/
printf("%c",c_temp);
}
printf("\n");
fclose(fp_names);
return;
}
/* End of function main */
```
```

# **Output:**

```
```text
Enter data you want to enter into a file, Press Ctrl+D at the end:
Anya Gangele
Harshit Jain

 Printing contents of file . . . . . . . . . .
Anya Gangele
Harshit Jain
```
```

In Program 2, a file pointer named fp_names is defined to be of type FILE. Then a file named names.txt is opened in write mode. If file exists, its existing contents will be destroyed. If the file does not exist, a new file named names.txt will be created. Characters from the user are accepted with function getchar. This function accepts character and the character is written in the file using the function fputc. When the user presses the Ctrl + d keys, −1 is returned by the function getchar, which is the value of EOF. The while loop stops there. Once writing work is over, the file names.txt is closed by passing its associated file pointer fp_names in function fclose.

The file names.txt is again reopened using the function fopen in reading mode. The program then reads the file content character by character with the function fgetc. The character that is returned by the function fgetc is then displayed on the screen. As discussed earlier, the function fgetc will advance the file pointer by one character. When the function fgetc encounters EOF marker, reading is terminated. The file is then closed with function fclose.

Execute Program 2 twice. You might have noticed that old contents of the file gets lost and new contents are written in the file. To retain the contents, open the names.txt file in append mode. Change the mode *w* to mode *a* in the statement fp_names=fopen ("names.txt","W"); Thus, the new statement will be fp_names=fopen("names.txt","a"); Recompile the program and execute it. Type Shalini Gangele. You will find that the typed contents are transferred to the file. The file is read again and the contents are displayed back on the screen. Execute the program once again. Type Puja Sethia. The name recently typed on the screen will be transferred to the file. However, when the file is opened for reading and its contents are displayed on the screen, both the names are displayed. This shows that new contents are appended at the EOF without overwriting the old contents.

# **13.6 String and File**

Program 2 transferred one character at a time to a disk file. Similarly, when the file was read, single character was read at a time. The functions fgetc and fputc are useful when