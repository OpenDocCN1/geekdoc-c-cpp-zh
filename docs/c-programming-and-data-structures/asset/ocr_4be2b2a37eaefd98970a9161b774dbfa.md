# 4.50 Computer Programming

```
printf(" 0 --------------------------\n");
for ( x = 0; x < 5; x = x+0.25 )
/* BEGINNING OF FOR LOOP */
y1 = (int) (50 * exp(-a * x) + 0.5);
y2 = (int) (50 * exp(-a * x/2) + 0.5);
/*......Plotting when y1 = y2......*/
if ( y1 == y2 )
{
if ( x == 2.5 )
printf(" X |");
else
printf("");
for ( i = 1; i <= y1 - 1; ++i )
printf("*");
printf("\n");
}
continue;
/*......Plotting when y1 > y2......*/
if ( y1 > y2 )
{
if ( x == 2.5 )
printf(" X |");
else
printf("");
for ( i = 1; i <= y1 - 2; ++i )
printf("*");
printf("\n");
}
continue;
/*......Plotting when y2 > y1......*/
if ( y2 > y1 )
{
if ( x == 2.5 )
printf(" X |");
else
printf("");
for ( i = 1; i <= y1 - 1; ++i )
printf("*");
printf("\n");
}
printf("\n");
} /* END OF FOR LOOP */
printf("\n");

```