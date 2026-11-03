```
file_ptr = fopen("farewell.txt", "r+a");
```

![](bbox=[0.28, 0.13, 0.73, 0.23])

Now, output a message to confirm the attempt succeeded

```
if(file_ptr != NULL)
{
    printf("File farewell.txt opened\n");
}
```

Next, in the if block, read and output all lines from the file

```
while( fgets( text, 50, file_ptr ) ) { printf( "%s", text ); }
```

Now, in the if block, copy a new string to the array then append that string to the text file

```
strcpy( text, "...by Lord Alfred Tennyson" );
fputs( text, file_ptr );
```

Finally, in the if block, close the file and return the required zero integer value

```
fclose( file_ptr );
return 0;
```

Add an alternative message if the attempt fails

```
else { printf( "Unable to open file\n" ); return 1; }
```

Save the program file, then compile and execute the program to open the file and append the text string

![](bbox=[0.28, 0.68, 0.73, 0.83])