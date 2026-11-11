| student[0].subject 1 | 45 |
| --- | --- |
| .subject 2 | 68 |
| .subject 3 | 81 |
| student[1].subject 1 | 75 |
| .subject 2 | 53 |
| .subject 3 | 69 |
| student[2].subject 1 | 57 |
| .subject 2 | 36 |
| .subject 3 | 71 |

**Fig. 12.3**  *The array student inside memory*

```
Program

struct marks
{
    int sub1;
    int sub2;
    int sub3;
    int total;
};
main()
{
    int i;
    struct marks student[3] = {{45,67,81,0},
                               {75,53,69,0},
                               {57,36,71,0}};

    struct marks total;
    for(i = 0; i <= 2; i++)
    {
        student[i].total = student[i].sub1 +
                           student[i].sub2 +
                           student[i].sub3;
        total.sub1 = total.sub1 + student[i].sub1;
        total.sub2 = total.sub2 + student[i].sub2;
        total.sub3 = total.sub3 + student[i].sub3;
        total.total = total.total + student[i].total;
    }
    printf(" STUDENT     TOTAL\n\n");
    for(i = 0; i <= 2; i++)
```