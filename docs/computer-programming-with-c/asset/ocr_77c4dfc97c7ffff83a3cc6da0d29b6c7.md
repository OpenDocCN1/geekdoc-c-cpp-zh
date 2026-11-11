```
```c
int i,j,k,max_length,lenI,lenJ;
char t;
for(i=0;i<=n-2;i++)
{
    for(j=i+1;j<=n-1;j++)
    {
        if(isGreater(a[i],a[j]))
        {
            lenI=strlen(a[i]);
            lenJ=strlen(a[j]);
            if(lenI>lenJ)
            {
                max_length=lenI;
            }
            else
            {
                max_length=lenJ;
            }
            for(k=0;k<max_length;k++)
            {
                t=a[i][k];
                a[i][k]=a[j][k];
                a[j][k]=t;
            }
        }
    }
}
} /*End of function sort() */
int isGreater(char p[],char q[])
{
    if(strcmp(p,q)>0)
    {
        return 1;
    }
    else
    {
        return 0;
    }
}
```
```

# Output

How many words are to be stored inside the array
4
Enter 4 words