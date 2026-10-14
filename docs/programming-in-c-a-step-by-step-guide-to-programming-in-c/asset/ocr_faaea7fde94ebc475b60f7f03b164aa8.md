open stream to show the end-of-file and error status of the stream. The Random Access functions allow control over the implied read/write position in the file. The *command line argument* is a parameter supplied to a program when the program is invoked.

# 13.9 Terminal Questions

1.The skeletal outline of a C program is shown below:

```
#include <stdio.h>
main()
{

FILE *pt1, *pt2; char name[20];

pt1 = fopen("sample.old", "r"); pt2= fopen("sample.new","w");..........
fclose(pt1);
fclose(pt2);
}
```

a)Read the string represented by name from the data file sample.old. b)Display it on the screen c)Enter the updated string. d)Write the new string to the data file sample.new

2.What is a command line argument and what is its use? Explain