```
4: {
5:   printf("Keep looking!" );
6:   printf("You\ll find it!\n");
7:   return 0;
8: }
```

5. BUG BUSTER: The following program has a problem. Enter it in your editor and compile it. Which lines generate problems?

```
1: #include <stdio.h>
2: 
3: int main( void )
4: {
5:   printf("This is a program with a " );
6:   do_it("problem!");
7:   return 0;
8: }
```

6. Make the following change to the program in exercise 3. Recompile and rerun this program. What does the program do now?

```
9: printf("%c", 1 );
```