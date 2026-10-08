```
/*
* Computed Variables:
/
* stress - compression stress (lb/in²)
* strain - nondimensional
/
* Output Variables:
/
* load - compression load (pounds)
* diameter - diameter of steel rods(inches)
* stress - compression stress (lb/in²)
* strain - nondimensional
*/****************************************************************
```

```
#include <stdio.h>
FILE *outptr;

int main ()
{
    const float PI = 3.141593;
    const float ES = 300000000;
    float load, diameter, area, stress, strain;

    outptr = fopen("fileout.dat", "w");

    for(load = 50000; load <= 100000; load += 25000)
    {
        fprintf(outptr,"\nCompression Load = %10.2f\n\n", load);
        fprintf(outptr,"Diameter      Stress      Strain\n", diameter, stress, strain);
        for(diameter = 2.0; diameter <= 5.0; diameter += 1.0)
        {
            area = (PI * diameter * diameter) / 4.0;
            stress = load / area;
            strain = stress / ES;
            fprintf(outptr,"%5.2f      %8.2f      %8.6f\n", diameter, stress, strain);
        }
    }
```