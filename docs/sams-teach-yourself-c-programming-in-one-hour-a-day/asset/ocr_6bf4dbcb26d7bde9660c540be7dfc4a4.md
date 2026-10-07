# LESSON 2 The Components of a C Program

This goes for your C source code as well. A simple typographical error in your program can cause the C compiler to choke, gag, and collapse. Fortunately, although the compiler isn't smart enough to correct your errors (and you'll make errors—everyone!), it is smart enough to recognize your errors as errors and report them to you. (You saw in Lesson I how the compiler reports error messages and how you interpret them.)

# A Review of the Parts of a Program

Now that all the parts of a program have been described, you can look at any program and find some similarities. Look at Listing 2.2 and see whether you can identify the different parts.

# Input

Listing 2.2 list_it.c – A Program to List a Code Listing with Added Line Numbers

```
1:  /* list_it.c This program displays a listing with line numbers! * */
2:  #include <stdio.h>
3:  #include <stdlib.h>
4:  #define BUFF_SIZE 256
5:  void display_usage(void);
6:  int line;
7: 
8:  int main(int argc, char *argv[])
9:   {
10:      char buffer[BUFF_SIZE];
11:      FILE *fp;
12: 
13:      if (argc < 2)
14:       {
15:          display_usage();
16:          return (1);
17:      }
18: 
19:      if ((fp = fopen(argv[1], "r")) == NULL)
20:       {
21:          fprintf(stderr, "Error opening file, %s!", argv[1]);
22:          return (1);
23:      }
24: 
25:      line = (1);
26: 
27:      while (fgets(buffer, BUFF_SIZE, fp) != NULL)
28:          fprintf(stdout, "%4d:\t%s", line++, buffer);
29: 
30:      fclose(fp);
31:      return 0;
32: }
```