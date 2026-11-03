```
ans = power(n,p);
printf("%d",ans);
getch();
}
int power(int n, int p)
{
    int ans=1, i;
    for(i=1;i<=p;i++)
    {
        ans = ans * n;
    }
    return(ans);
}
```

# Function whose argument is a two dim array:-

```
void mat_sum(int m1[][10], int r1, int c1, int m2[][10], int r2, int c2, int m3[][10])
{
    int i,j;
    if(r1 != c1 && r2 != c2)
    {
        printf("Can't sum");
        exit();
    }
    for(i=0;i<r1;i++)
        for(j=0;j<c1;j++)
            m3[i][j] = m1[i][j] + m2[i][j];
}
```

The above function can be called from main() as mat_sum(m1,r1,c1,m2,r2,c2,m3);

# Recursion -

A function is called recursive if a statement within the body of a function calls the same function. Sometimes called as 'circular definition', recursion is a function calling itself in the definition. A recursive function should have two parts recursive statement & a termination condition.