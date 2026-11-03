![](bbox=[0.05, 0.05, 0.95, 0.28])

Here each condition is checked, and when a condition is found to be true, the statements corresponding to that are executed, and the control comes out of the nested structure without checking remaining conditions. If none of the conditions is true then the last else part is executed.

```
/*P5.6 Program to find out the grade of a student when the marks of 4 subjects are given. The method of assigning grade is as-
per<85 grade=A
per<70 and per>55 grade=B
per<55 and per>40 grade=C
per<40 grade=E
Here per is percentage.
*/
#include<stdio.h>
main()
{
float m1,m2,m3,m4,total,per;
char grade;
printf("Enter marks of 4 subjects : ");
scanf("%f%f%f%f",&m1,&m2,&m3,&m4);
total=m1+m2+m3+m4;
per=total/4;
if(per>=85)
grade='A';
else if(per>=70)
grade='B';
else if(per>=55)
grade='C';
else
grade='E';
}
```