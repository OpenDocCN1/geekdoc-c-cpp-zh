# 1.86 Computer Programming

```
Program
main()
{
int a,b,c,x,y,z;
int p,q,r;
printf("Enter three integer numbers\n");
scanf("%d %d %d",&a,&b,&c);
printf("%d %d %d\n",a,b,c);
printf("Enter two 4-digit numbers\n");
scanf("%2d %d",&x,&y);
printf("%d %d\n",x,y);
printf("Enter two integers\n");
scanf("%d %d",&a,&x);
printf("%d %d\n",a,x);
printf("Enter a nine digit number\n");
scanf("%3d %d",&q,&r);
printf("%d %d\n",q,r);
printf("Enter two three digit numbers\n");
scanf("%d %d",&x,&y);
printf("%d %d\n",x,y);
}

```

```
Output

Enter three integer numbers
1 2 3
1 3 -357
Enter two 4-digit numbers
6789 4321
67 89
Enter two integers
44 66
4321 44
Enter a nine-digit number
123456789
66 1234
Enter two three-digit numbers
123 456
89 123
```

![](bbox=[0.05, 0.6, 0.95, 0.63])

The first scanf requests input data for three integer values a, b, and c, and accordingly three values 1, 2, and 3 are keyed in. Because of the specification %*d the value 2 has been skipped and 3 is assigned to the variable b. Notice that since no data is available for c, it contains garbage.

The second scanf specifies the format %2d for the variables x and y respectively. Whenever we specify field width for reading integer numbers, the input numbers should not contain more digits than the specified size. Otherwise, the extra digits on the right-hand side will be truncated and assigned to the next variable in the list. Thus, the second scanf has truncated the four digit number 6789 and assigned 67 to x and 89 to y. The value 4321 has been assigned to the first variable in the immediately following scanf statement.