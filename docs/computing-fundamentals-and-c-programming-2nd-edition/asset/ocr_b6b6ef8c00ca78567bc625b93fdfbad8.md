```
```c
printf(" Week(%d)\t", i);
for(j=1; j <=5; j++)
    printf("%7d", Mvalue[i][j]);
printf("\n");
}
printf("\n VALUE MATRIX OF SALES\n\n");
for(i=1; i <=4; i++)
{
    printf(" Week(%d)\t", i);
    for(j=1; j <=5; j++)
        printf("%7d", Svalue[i][j]);
    printf("\n");
}
break;
/* WEEKLY ANALYSIS */
case 2:
    printf(" TOTAL WEEKLY   PRODUCTION & SALES\n\n");
    printf("                 PRODUCTION   SALES\n");
    printf("                 ----------   --  \n");
    for(i=1; i <=4; i++)
    {
        printf(" Week(%d)\t", i);
        printf("%7d\t%7d\n", Mweek[i], Sweek[i]);
    }
    break;
/* PRODUCT WISE ANALYSIS */
case 3:
    printf(" PRODUCT WISE TOTAL PRODUCTION &");
    printf(" SALES\n\n");
    printf("                 PRODUCTION SALES\n");
    printf("                 ---------- -- \n");
    for(j=1; j <=5; j++)
    {
        printf(" Product(%d)\t", j);
        printf("%7d\t%7d\n", Mproduct[j], Sproduct[j]);
    }
    break;
/* GRAND TOTALS */
case 4:
    printf(" GRAND TOTAL OF PRODUCTION & SALES\n");
    printf("\n Total production = %d\n", Mtotal);
    printf(" Total sales = %d\n", Stotal);
```
```