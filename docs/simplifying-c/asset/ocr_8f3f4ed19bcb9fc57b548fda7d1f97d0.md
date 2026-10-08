```
/* declaring file pointer */
FILE *fp_names;

/* Opening a file names.txt in writing mode*/
fp_names=fopen("names.txt","w");
if (fp_names == NULL)
{
printf("File could not be opened successfully.........\n");
exit(1);
}
printf("\nEnter data you want to enter into a file, Press Ctrl+D at the end: ");

/* Accepting character from keyboard */
while ((c_temp=getchar())!=EOF)
{
/* writing characters to a file */

fputc(c_temp,fp_names);
}

/* Closing a file */
fclose(fp_names);

/* Opening a file in reading mode*/
fp_names=fopen("names.txt", "r");
if (fp_names == NULL)
{
printf("File could not be opened successfully........");
exit(1);
}
printf("\n Printing contents of file...............\n");

/* Reading characters from a file*/
while ((c_temp=fgetc(fp_names))!=EOF)
{
/* Displaying characters in screen*/
printf("%c",c_temp);
}
printf("\n");

/* Usage of eof() function */
if (feof(fp_names))
printf("End of file was reached.\n");

else
printf("Unread records are remaining in the file\n");

fclose(fp_names);
return;
}
/* End of function main */
```