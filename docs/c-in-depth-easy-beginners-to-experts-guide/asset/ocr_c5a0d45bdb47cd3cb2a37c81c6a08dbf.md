| [0] | [0] | [0] | [0] | [1] | [1] | [1] | [1] | [2] | [2] | [2] | [2] | [3] | [3] |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [0] | [1] | [2] | [3] | [0] | [1] | [2] | [3] | [0] | [1] | [2] | [3] | [0] | [1] |
| 10 | 5 | 6 | 7 | 36 | 94 | 56 | 29 | 83 | 67 | 12 | 69 | 86 | 39 |
| 100 | 102 | 104 | 106 | 108 | 110 | 112 | 114 | 116 | 118 | 120 | 122 | 124 | 126 |

# SOME SOLVED PROGRAMS -

# 1. WAP to transpose a 2-d array.

```
#define maxrow 10
#define maxcol 10
main()
{
    int m[maxrow][maxcol],i,j,row,col;
    clrscr();
    printf("Enter number of rows and columns in the matrix: ");
    scanf("%d %d",&row,&col);
    for(i=0;i<row;i++)
    {
        for(j=0;j<col;j++)
        {
            printf("Enter element %d,%d: ",i+1,j+1);
            scanf("%d",&m[i][j]);
        }
    }
    /*To print the matrix as input by the user*/
    printf("Matrix input:\n\n");
    for(i=0;i<row;i++)
    {
        for(j=0;j<col;j++)
            printf("%d\t",m[i][j]);
        printf("\n");
    }
    /*transpose*/
    printf("\n\nTransposed matrix\n\n");
    for(i=0;i<col;i++)
    {
        for(j=0;j<row;j++)
            printf("%d\t",m[j][i]);
        printf("\n");
    }
    getch();
}
```