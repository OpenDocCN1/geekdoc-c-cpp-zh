```
printf("Student[%d]      %d\n", i+1,student[i].total);
printf("\n SUBJECT      TOTAL\n\n");
printf("%s           %d\n%s      %d\n",
       "Subject 1  ", total.sub1,
       "Subject 2  ", total.sub2,
       "Subject 3  ", total.sub3);

printf("\nGrand Total = %d\n", total.total);
}

Output

STUDENT          TOTAL
Student[1]       193
Student[2]       197

Student[3]       164

SUBJECT          TOTAL
Subject 1        177
Subject 2        156
Subject 3        221

Grand Total   = 554
```

**Fig. 12.4** *Arrays of structures: Illustration of subscripted structure variables*

# ## 12.8 ARRAYS WITHIN STRUCTURES   **LO 12.4**

C permits the use of arrays as structure members. We have already used arrays of characters inside a structure. Similarly, we can use single-dimensional or multi-dimensional arrays of type **int** or **float**. For example, the following structure declaration is valid:

```
struct marks
{
    int number;
    float subject[3];
} student[2];
```

Here, the member **subject** contains three elements, **subject[0]**, **subject[1]**, and **subject[2]**. These elements can be accessed using appropriate subscripts. For example, the name 
`student[1].subject[2];`
 would refer to the marks obtained in the third subject by the second student.