```
int i_base, i_height, i_area;
/* Accept the value of base and height */

printf("\n Enter the value of base of triangle: ");
scanf("%d",&i_base);
printf("\n Enter the value of height of triangle: ");
scanf("%d",&i_height);

/* Calculate are of triangle */
i_area = (i_base * i_height) / 2;

/* Print Area */
printf("\nArea of triangle with base %d and height %d is %d\n",
i_base,i_height,i_area);
return;
}

/* End of Program */
```

Output 1:

```
Enter the value of base of triangle: 10
Enter the value of height of triangle: 15
Area of triangle with base 10 and height 15 is 75
```

Output 2:

```
Enter the value of base of triangle: 5
Enter the value of height of triangle: 15
Area of triangle with base 5 and height 15 is 37
```

Note the usage of i_ in the preceding program, the prefix i_ is an indication that variable i_base, i_height and i_area are of type integer data type. Similarly prefix f_ is used for float data type, c_ is used for character data type and so on.

Every figure contains a descriptive caption to clarify:

![](bbox=[0.32, 0.62, 0.82, 0.84])

▲ Figure 1: Flowchart of the Voting Eligibility Problem