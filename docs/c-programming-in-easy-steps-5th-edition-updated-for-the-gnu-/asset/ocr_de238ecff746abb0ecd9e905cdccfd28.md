```
```c
printf("Char cast to int: %d in", (int)letter );
printf("Int cast to char: %c in", (char)zee );
printf("Float arithmetic: %f in", (float)x / (float)y );
printf("Double cast to float: %f in", (float)decimal );
```
```

+   4. At the end of the function block, return a zero integer value, as required by the function declaration return 0 ;
+   5. Save the program file, then compile and execute the program to see the resulting equivalent from each cast

```
C:\MyPrograms>gcc cast.c -o cast.exe
C:\MyPrograms>cast
Float cast to int: 5
Char cast to int: 65
Int cast to char: Z
Float cast to char: 0
Float arithmetic: 1.400000
Double cast to Float: 0.123457
C:\MyPrograms>_
```

Values cast from a float to an int get truncated but those cast from a double to a float get rounded.