```
/* fscanf_fprintf.c: Uses (i) fprintf to append user input to a file,
                     (ii) fscanf to read the entire file. */
#include <stdio.h>
#include <stdlib.h>
#define FLUSH_BUFFER while (getchar() != '\n') ;

int main(void)
{
    FILE *fp;
    char name[20];
    short marks1, marks2, total;

    if ((fp = fopen("foo", "a+")) == NULL) {     /* File will also be read */
        perror("");
        exit(2);
    }

    do {
        fprintf(stderr, "Student name: ");
        if (fscanf(stdin, "%[^\n]", name) != 1)
            break;                  /* Quits loop when only [Enter] is pressed */

        fprintf(stderr, "Marks in 2 subjects: ");
        fscanf(stdin, "%hd%hd", &marks1, &marks2);

        FLUSH_BUFFER

        fprintf(fp, "%s:%hd:%hd:%hd\n",             /* Writes a line to file */
                name, marks1, marks2, marks1 + marks2);
    } while (1);

    rewind(fp);
    while (fscanf(fp, "%[^:]:%hd:%hd:%hd",          /* Reads each line */
                  name, &marks1, &marks2, &total) == 4)
        fprintf(stdout, "%-20s %3hd %3hd %3hd\n", name, marks1, marks2, total);
    exit(0);
}
```

# PROGRAM 15.7: **fscanf_fprintf.c**

```
Student name: Larry Ellison
Marks in 2 subjects: 65 75
Student name: Jeff Bezos
Marks in 2 subjects: 75 85
Student name: Elon Musk
Marks in 2 subjects: 90 95
Student name: [Enter]
Larry Ellison         65  75 140
Jeff Bezos            75  85 160
Elon Musk              90  95 185
```

PROGRAM OUTPUT: **fscanf_fprintf.c**