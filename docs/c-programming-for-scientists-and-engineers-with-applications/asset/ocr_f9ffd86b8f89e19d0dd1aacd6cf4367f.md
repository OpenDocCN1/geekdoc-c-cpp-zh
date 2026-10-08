```
/* Output Parameters:
/*   unitcost1[n] - cost of each unit
/* */
/*
********************************************************************
void funccompute(int partunits1[], float unitcost1[],
      float unitcost1[],int n)
{
    int i;
    for(i = 0; i < n; i++)
    {
        unitcost1[i] = partunits1[i] * unitcost1[i];
    }
    return;
}
********************************************************************
/* */
/*   functotunits: Compute Total Units of All Parts
/* */
********************************************************************
/* */
/* Input Parameters:
/*   partunits1[n] - number of units
/*   n - number of parts
/* */
/*   Computed Variables:
/*   totalunits - total units of all parts
/* */
/*   Returned Variables:
/*   totalunits - total units of all parts
/* */
********************************************************************
int functotunits(int partunits1[],int n)
{
    int i, totalunits = 0;
    for(i = 0; i < n; i++)
    {
        totalunits += partunits1[i];
    }
    return totalunits;
}
********************************************************************
/* */
/*   functotcost: Compute Total Cost of All Parts
/* */
```