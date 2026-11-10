```
abcdef…
mnop qrst
uvwxyz

PROGRAM INPUT: Contents of foo
$ a.out
Not enough arguments
$ a.out foo
Size of file = 29

zyxwvu
tsrqponm
lkjihgfedcba

Effect of \\n at end of foo
The first line in reverse
```

PROGRAM OUTPUT: **reverse_read.c**

**Tip:** As with some of the previous programs, this program can be redirected (using, say, `a.out > bar`) when run from the OS shell. The reversed output of foo would then be saved in bar. But the messages would still appear on the terminal because they write to `stderr`, which is unaffected by redirection. Whenever possible, programs should be designed to behave in a flexible manner.

# 15.15  `update_structure.c`: UPDATING A STRUCTURE STORED ON DISK

Program 15.14 highlights the advantages of using `fread` and `fwrite` with structures. It accesses the five structures saved in the file `student.dat` in Program 15.12. The current program searches this database for a specific record and updates it with user-input data. The updated contents of the binary database are finally displayed in text form. Like in a previous program, all messages barring one are directed to the standard error. Thus, this program can also be used with redirection to save the output—but only to a *text* file.

```
/* update_structure.c: Uses fseek, ftell, fread and fwrite
   to update a structure saved in a file. */
#include <stdio.h>
#include <stdlib.h>
#define COLUMNS 5
int main(void)
{
    FILE *fp;
    struct student {
        char name[30];
        int roll_no;
        short marks;
    } stud;
    short i, s_marks, found = 0, records;
    int size, s_roll_no;
```