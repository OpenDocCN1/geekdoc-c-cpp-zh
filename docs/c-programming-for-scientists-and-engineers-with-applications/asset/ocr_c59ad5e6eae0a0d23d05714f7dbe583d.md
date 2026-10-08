# 11.3 Structures and Functions 703

```
#include <stdio.h>
struct column
{
    float diameter;
    float compload;
    float stress;
    float strain;
};
defef struct column COLUMN;
```

```
float fnstress(COLUMN);
double fnstrain(COLUMN);
void foutput(COLUMN)
int main()
{
    struct column steelcol;
    scanf("%%f %f", &steelcol.diameter,&steelcol.compload);
    steelcol.stress = fnstress(steelcol);
    steelcol.strain = fnstrain(steelcol);
    foutput(steelcol);
    return 0;
}
```

```
float fnstress(COLUMN steelcolumn1)
{
    const float PI = 3.141593;
    float area, tempstress;
    area = (PI * steelcolumn1.diameter * steelcolumn1.diameter)/4.0;
    tempstress = steelcolumn1.compload / area;
    return tempstress;
}
```

```
double fnstrain(COLUMN steelcolm1)
{
    const float E = 30000000.00;
    double tempstrain;
    tempstrain = steelcolm1.stress / E;
```