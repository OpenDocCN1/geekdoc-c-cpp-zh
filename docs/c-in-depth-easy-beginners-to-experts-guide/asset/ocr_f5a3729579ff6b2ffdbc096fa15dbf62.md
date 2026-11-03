```
while(n != -1)
{
    printf("Enter number %d ",i++);
    scanf("%d",&n);
    if(n < prev && n != -1)
        flag=false;
    prev=n;
}
if(flag == false)
    printf("Not in ascending order");
else
    printf("In ascending order");
```

# 6. To print the sum of 9+99+999+............ n terms.

```
long int term,sum=0;
int n,cnt;
clrscr();
printf("Enter the value of n");
scanf("%d",&n);
for(cnt=1,term=9;cnt<=n;cnt++)
{
printf("%ld\n",term);
sum+=term;            /*adding the term to sum using assignment operator*/
term=(term*10) + 9;
}
printf("%ld",sum);
```

# 7.

```
/*pascal triangle
1
11
121
1331
14641 */
```

```
main()
{
int i,j,n,b; /*b=preceding no*/
printf("enter the number of rows: ");
scanf("%d",&n);
for(i=0;i<n;i++)
```