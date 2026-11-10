Write a program that uses `fscanf` to read and print only the third field. Repeat the exercise using `fgets` and `sscanf` and without closing foo.

15.16  A file foo contains the following lines:

Gagarin 23-12-1927
Glenn Dec-31-17
Armstrong 20-Jun-29

Write a program that scans each line with `sscanf` and writes the lines to a file bar using the format dd-mm-yy for the date field.

15.17  Correct the following program and explain why it still prints a line of foo after invoking the `remove` function.

```
```c
#include <stdio.h>
#include <string.h>
int main(void)
{
    char buf[80];
    FILE *fp = fopen("foo", 'r');
    remove("foo");
    fgets(fp, buf, 80);
    fprintf("%s\n", buf, stdout);
    return 0;
}
```
```

15.18  Write a program that deletes all files whose names are provided as command-line arguments.