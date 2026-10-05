# ARRAYS

```
printf("nAfter the operation .. \n");
printf("The array3's contents. \n");
for (i = 0; i<3; i++)
{
    for (j=0;j<3; j++)
    {
        printf("%d\t", array3[i][j]);
    }
    printf("\n");
}
printf("Choose the operation to be performes on arrays..")
\n1.Add\t2.Subtract\t3.Multiply\n");
scanf("%d", &choice);
while(choice<=3)
{
    getch();
}
```

# Program 3.6 Matrix Operations part III

As it can be observed from Program 3.6, 2-D arrays are similar to 1-D arrays except the fact that they have 2 subscripts, and accessed with two loops. Rest of the properties are same as 1-D arrays. [Care should be taken during matrix multiplication to ensure the property that the column size of first matrix and the row size of second should be the same.]

![](bbox=[0.095, 0.477, 0.882, 0.893])