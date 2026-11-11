```
```cpp
n = d1.n + d2.n;
int i=1,j=1,k=1;

while((i<=d1.n) && (j<=d2.n))
{
    if(d1.a[i] < d2.a[j])
    {
        a[k]=d1.a[i];
        ++i;
        ++k;
    }
    else
    {
        a[k] = d2.a[j];
        ++k;
        ++j;
    }
}

while(i<=d1.n)
{
    a[k]=d1.a[i];
    ++i;
    ++k;
}

while(j<=d2.n)
{
    a[k]=d2.a[j];
    ++j;
    ++k;
}
}

void dmani :: sort()
{
    int sorted=0;
    int k=0;
    int temp;

    for(k=1;k<=n-1;k++)    /* For sorting the array for n-1 passes*/
    {
```
```