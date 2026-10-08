```
{
  if(fabs(expdata[i] - mean) > stddev)
    printf("%.2f\n", expdata[i]);
  }
  return 0;
}
```

```
/**********************************************************************************/
/* Function: funcmean - Computes the Mean                             */
/**********************************************************************************/
/* Input Parameters:                                                   */
/* expexpdata[n]- - Experimental data                                     */
/* n - number of data values                                           */
/* Local Variables:                                                      */
/* mean - mean value                                                     */
/* sum - sum of data values                                            */
/* Return value:                                                        */
/* mean - mean value                                                     */
/* Functions Called: none                                               */
/**********************************************************************************/
```

```
float funcmean(float expdata[ ], int n)
{
  int i;
  float sum = 0, mean;
  for(i = 0; i < n; i++)
    sum += expdata[i];
  mean = sum / n;
  return mean;
}
```

```
/**********************************************************************************/
/* Function: funcstdev - Computes the Standard                             */
/* Deviation                                                              */
/**********************************************************************************/
```