```
funcinput(depth);

printf("Measured Depths\n");
funcoutput(depth);
funcpressure(depth, pressure);
printf("Computed Pressure\n");
funcoutput(pressure);
averagepressure = funcavgpressure(pressure);
printf("Average Pressure: %6.2f\n", averagepressure);
return 0;
}
```

```
********************************************************************/
/* funcinput: Input the Measured Values of the */
/* Depth in Feet */
********************************************************************/
/* Output Parameters: */
/* depth1[][JMAX] - measured depth of water */
/*                   in feet */
/* Input Variables: */
/* depth1[][JMAX] - measured depth of water */
/*                   in feet */
********************************************************************/
```

```
void funcinput(float depth1[][JMAX])
{
  FILE *inptr;
  int i, j;

  inptr = fopen("depth.dat", "r");
  for(i = 0; i < IMAX; i++)
    for(j = 0; j < JMAX; j++)
      sscanf(inptr, "%f", &depth1[i][j]);

  fclose(inptr);
  return;
}
```