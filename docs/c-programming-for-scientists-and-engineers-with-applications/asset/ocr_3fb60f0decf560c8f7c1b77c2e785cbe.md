# 518  Multidimensional Arrays

```
float funcavgpressure(float pressure[] ][JMAX)
{
    int i, j;
    float sumpressure = 0.0;
    float average_pressure = 0;

    for(i = 0; i < IMAX; i++)
        for(j = 0; j < JMAX; j++)
            sumpressure += pressure[i][j];

    average_pressure = (sumpressure / (IMAX * JMAX));
    return average_pressure;
}

return;
}
```

> ********************************************************/
/*
/* Function: funcoutput()                                     */
/*   Output the Depth and Pressure                           */
/*********************************************************/
/*
/*   Input Parameters:                                        */
/*   array1[] ][JMAX] - dummy array replaced by the */
/*   depth and pressure arrays                            */
/*
/*   Output Variables:                                        */
/*   array[] ][JMAX] - dummy array replaced by the */
/*   depth and pressure arrays                            */
/*
********************************************************/

```
void funcoutput(float array1[] ][JMAX)
{
    int i, j;
    for(i = 0; i < IMAX; i++)
    {
        for(j = 0; j < JMAX; j++)
        {
            printf("%6.2f ", array1[i][j]);
        }
        printf("\n");
    }
}
```