```
}
record.average = record.sum / 4.0;

if(record.average >= 90.0)
    record.ltgrd = 'A';
else if(record.average >= 80.0)
    record.ltgrd = 'B';
else if(record.average >= 70.0)
    record.ltgrd = 'C';
else if(record.average >= 60.0)
    record.ltgrd = 'D';
else
    record.ltgrd = 'F';

printf("%s %s\n", record.sid, record.name);
for(i = 0; i < 4; i++)
    printf("%d %5.2f\n", i, record.score[i]);
printf("%5.2f %c\n\n", record.average, record.ltgrd);

return 0;
```

The following example shows the input and output of structure variables of data int, float, char, arrays, and character strings. This program uses a pointer to the structure variable and the member dereference operator (-).

#include <stdio.h>

```
struct strec
{
    char stid[6];
    char name[20];
    int score[4];
    float sum;
    float average;
    char ltgrd;
};

FILE *inptr;
int main()
{
    struct strec record, *stptr;
```