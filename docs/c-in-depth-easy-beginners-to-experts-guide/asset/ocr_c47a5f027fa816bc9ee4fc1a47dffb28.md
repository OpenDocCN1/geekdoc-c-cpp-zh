```
sum=sum*2;
} while(index>9);
```

# Answers —

1. initialization,condition,increment    2. b    3. b    4. b    5. C
6. 1,2,3...32767, -32768,...infinite loop    7. 5    8. 2

# SOME SOLVED PROGRAMS -

# 1. Print the numbers in reverse order from N to 1

N...........5, 4, 3, 2, 1

```
int i,n;
printf("Enter the value of N ");
scanf("%d",&n);
for(i=n;i>=1;i--)
printf("%d,",i);
printf("\b ");    /*To remove the comma (,) printed at the last */
```

# 2. Print the Fibonnicci series1, 1, 2, 3, 5, 8, 13,.................N

```
int prev,next,cnt,sum,n;
printf("Enter the value of N ");
scanf("%d",&n);
prev=0;
next=cnt=1;
while(cnt<=n)
{
    printf("%d,",next);
    sum = prev + next;
    prev = next;
    next = sum;
```