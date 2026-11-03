```
```c
int d1,m1,y1,d2,m2,y2;
splitDate(date1,&y1,&m1,&d1);
splitDate(date2,&y2,&m2,&d2);
if(d2<d1)
{
    if(m2==3)
    {
        if(isLeap(y2))
            d2=d2+29;
        else
            d2=d2+28;
    }
    else if(m2==5 || m2==7 || m2==10 || m2==12)
        d2=d2+30;
    else
        d2=d2+31;
    m2=m2-1;
}
if(m2<m1)
{
    y2=y2-1;
    m2=m2+12;
}
*y=y2-y1;
*m=m2-m1;
*d=d2-d1;
/*End of diffYMD*/
```
```

The logic of this function is similar to that given in program P5.37.

# 15.4.9 Diffdays.c

```
```c
/*To get difference of two dates in days*/
int diffDays(char *date1,char *date2)
{
    int d1,m1,y1,d2,m2,y2,j1,j2;
    int y,d,i,days;
    d=0;
    splitDate(date1,&y1,&m1,&d1);
    splitDate(date2,&y2,&m2,&d2);
    j1=julian(d1,m1,y1);
    j2=julian(d2,m2,y2);
    if(y1==y2)
        return (j2-j1);
    for(i=y1+1;i<y2-1;i++)
    {
        if(isLeap(i))
            d=d+366;
        else
            d=d+365;
    }
    if (isLeap(y1))
```
```