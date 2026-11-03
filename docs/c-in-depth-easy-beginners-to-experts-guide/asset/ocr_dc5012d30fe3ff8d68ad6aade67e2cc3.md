```
printf("\n Plz Enter second distance.");
printf("\n Plz Enter the feets");
scanf("%f",&d2.feet);
printf("\n Plz Enter the inches");
scanf("%f",&d2.inch);

d3.feet=d1.feet+d2.feet;
d3.inch=d1.inch+d2.inch;

while(d3.inch>=12)
{
    d3.feet++
    d3.inch=d3.inch-12;
} printf("\n sir After Adition both parts");
printf("\n feet = %f,inches=%f",d3.feet,d3.inch);
getch();
}
```

# 107. Wap to create a Date structure and increase date by Addition No. of days and date should be valid.

```
#include<stdio.h>
#include<conio.h>
struct date
{
    int dd,mm,yy;
};
void main()
{
    struct date d;
```