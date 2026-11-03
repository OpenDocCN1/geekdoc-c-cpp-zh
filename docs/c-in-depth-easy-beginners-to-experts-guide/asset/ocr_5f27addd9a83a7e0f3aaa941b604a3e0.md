# Output: 200 100

Here in first two statements after declaration the first and last element is assigned with 100 and 200 respectively and the in next three statements swap both of them. So num[0] = 200 and num[25] = 100.

```
2. int array[26],i;
for (i = 0; i<=25;i++)
{
    array[i] = 'A' + i;
    printf("\n%d %c",array[i], array[i]);
}
```

Output:
65 A
66 B
-----
-----
90 Z

In the above program first time array of i will be 65 because i =0 and 'A' gives 65 so array[0] = 65 that gets printed through printf( ) in integer and character format. And each time when i increment by 1 the array will contain 66,67,68 on successive position and will print through printf( ) in integer and character format.

```
3. int sub[50],i;
for( i = 0; i <= 48; i++);
{
    sub[i] = i;
    printf("\n%d",sub[i]);
}
```

# Output: 49

Because of ";"(Null statement) the loop will execute till 48 without executing any statement and when i's

# Output:- 10 20 30 40 50

In the above program the base address of b is assign to the k through k = b statement. Because when we use the name of array it tells the base address of array. And loop runs 5 times in the above program and each time k deference the respective element and print it. And we know when pointer is incremented it moves the required bytes(in the above program moves 2 byte because it points to int array) and point the next element. Here first time k contains 0th element address and print it by deference and by increment it points to next element and because loop runs 5 times so five times pointer incremented and point the value starting from base address so it print all the array element.

```
6. main()
{
    int a [] = {2,6,4,8,10};
    int i;
    change( a, 5);
    for(i = 0;i<=4;i++)
        printf("%d ",a[i]);
}
change(int *b, int n)
{
    int i;
    for(i = 0;i<n;i++)
        *(b+i) = *(b+i)+5;
}
```

# Output:- 7 11 9 13 15

Here pointer b receive the base address of a and 5 is passed to n. and in the change( ) each time b[i] is