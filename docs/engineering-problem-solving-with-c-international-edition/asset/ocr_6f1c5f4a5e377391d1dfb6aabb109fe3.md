```
```c
if (dl)
{
    weight *= (formula[current+1]-'0');
    current += 2;
}
else
    current++;
}
total += weight;
}
else
    done = 1;
}
/* Print formula and weight. */
printf("Formula: %n");
for (k=0; k<=n; k++)
    putchar(formula[k]);
printf("\n");
if (done == 0)
    printf("Molecular Weight: %f \n",total);
else
    printf("Error in formula. \n");
/* Exit program. */
    return 0;
}
/*--------------------------------------------------*/
/*
/* This function returns the molecular weight of an element */
/* in an amino acid. */
/*
double atomic_wt(int atom)
{
    /* Declare and initialize variables. */
    int k=0, element[5]={'H', 'C', 'N', 'O', 'S'};
    double m_wt[5]={1.00794, 12.011, 14.00674,
    15.9994, 32.066}, weight;
/* Search for element. */
while (k<4 && element[k]!=atom)
    k++;
/* Return corresponding atomic weight. */
if (k < 4)
    weight = m_wt[k];
else
    weight = 0;
    return weight;
}
/*--------------------------------------------------*/
```
```