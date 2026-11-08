```
```c
printf("\n Enter array size");
scanf("%d",&n);
printf("Enter the Array Elements \n");
for(i=0;i<n;i++)
{
    printf("%d- ",i+1);
    scanf("%d",&num[i]);
}
for(i=0;i<n;i++)
{
for(j=i+1;j<n;j++)
{
if(num[i]>num[j])
{
temp=num[i];
num[i]=num[j];
num[j]=temp;
}
}
}
printf("\n The sorted list as follows");
for(i=0;i<n;i++)
{
    printf("\n %d",num[i]);
}
printf("\n The reverse sorted order\n");
for(i=n-1;i>=0;i--)
{
    printf("\n %d",num[i]);
}
getch();
}
```
```