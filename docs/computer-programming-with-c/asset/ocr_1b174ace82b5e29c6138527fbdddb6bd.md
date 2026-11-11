```
```c
void main()
{
int a[100],n,i,key,status;
float mean;
printf("Enter the number of elements to be stored in the array\n");
scanf("%d",&n);
    for(i=0;i<n;i++)
    {
        printf("Enter element number %d\n",i+1);
        scanf("%d",&a[i]);
    }
printf("Enter the element to be searched in the array\n");
scanf("%d",&key);
status = find(a,key,n);
    if(status==0)
    {
    printf("Element not found\n");
    }
    else
    {
    printf("Element found\n");
    }
}
int find(int a[],int x,int n)
{
int i=0;
    while(i<n && a[i]!=x)
    {
    i++;
    }
    if(i==n)
    {
    return 0;
    }
    else
    {
    return 1;
    }
}
```
```

# Output

```
```
Enter the number of elements to be stored in the array
5
Enter element number 1
10
```
```