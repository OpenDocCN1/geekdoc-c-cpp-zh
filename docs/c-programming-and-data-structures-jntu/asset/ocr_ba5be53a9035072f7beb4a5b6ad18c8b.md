# Example 7.4

A class of n students take an annual examination in m subjects. A program to read the marks obtained by each student in various subjects and to compute and print the total marks obtained by each of them is given in Fig. 7.5.

```
Program
/ ************************************************************/
/ * ILLUSTRATION ON NESTED LOOPS */
/ ************************************************************/
#define FIRST  360
#define SECOND 240
main()
{
 int n, m, i, j;
 roll-number, marks, total;
 printf("Enter number of students and subjects\n");
 scanf("%d %d", &n, &m);
 printf("\n");
 for (i = 1; i <= n; ++i)
 {
 printf("Enter roll-number: ");
 scanf("%d", &roll-number);
 total = 0 ;
 printf("Enter marks of %d subjects for ROLL NO %d\n",m,roll-number);
 for (j = 1; j <= m; j++)
 {
 scanf("%d", &marks);
 total = total + marks;
 }
 printf("TOTAL MARKS = %d", total);
 if (total >= FIRST)
 printf("(First Division) \n\n");
 else if (total >= SECOND)
 printf("(Second Division) \n\n");
 else
 printf("*** F A I L *** \n\n");
 }
}
```

Output
Enter number of students and subjects
3 6
Enter roll-number : 8701
Enter marks of 6 subjects for ROLL NO 8701
81 75 83 45 61 59
TOTAL MARKS = 404 ( First Division )
Enter roll-number : 8702
Enter marks of 6 subjects for ROLL NO 8702
51 49 55 47 65 41
TOTAL MARKS = 308 ( Second Division )
Enter roll-number : 8704
Enter marks of 6 subjects for ROLL NO 8704
40 19 31 47 39 25
TOTAL MARKS = 201 ( *** F A I L ***)

# Fig. 7.5 Illustration of nested for loops