# 3.16 Computer Programming

```
for ( j = 0 ; j < MAXITEMS ; j++ )
{
	scanf("%d", &value[i][j]);
	girl_total[i] = girl_total[i] + value[i][j];
}
/*.....COMPUTING item_total.............*/
for ( j = 0 ; j < MAXITEMS ; j++ )
{
	item_total[j] = 0;
	for ( i = 0 ; i < MAXGIRLS ; i++ )
	{
		item_total[j] = item_total[j] + value[i][j];
	}
}
/*.....COMPUTING grand_total.............*/
grand_total = 0;
for ( i = 0 ; i < MAXGIRLS ; i++ )
{
	grand_total = grand_total + girl_total[i];
}
/* .....PRINTING OF RESULTS.............*/
print("\n GIRLS TOTALS\n");
for ( i = 0 ; i < MAXGIRLS ; i++ )
{
	print("Salesgirl[%d] = %d\n", i+1, girl_total[i] );
}
for ( j = 0 ; j < MAXITEMS ; j++ )
{
	print("\nItem[%d] = %d\n", j+1, item_total[j] );
}
print("\nGrand Total = %d\n", grand_total);
```

# Output

Input data
Enter values, one at a time, row wise

+   310 257 365
+   210 190 325
+   405 235 240
+   260 300 380

# GIRLS TOTALS

+   Salesgirl[1] = 950
+   Salesgirl[2] = 725
+   Salesgirl[3] = 880
+   Salesgirl[4] = 940

# ITEM TOTALS

+   Item[1] = 1185
+   Item[2] = 1000
+   Item[3] = 1310

Grand Total = 3495

> Fig. 3.8 Illustration of two-dimensional arrays