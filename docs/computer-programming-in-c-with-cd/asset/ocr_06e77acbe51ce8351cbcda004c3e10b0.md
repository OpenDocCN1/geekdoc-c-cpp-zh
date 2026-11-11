Q9. Create a program that accepts basic salary of an employee and then displays his total salary, which includes D.A. 10%, HRA 25%, and PF 10.3% with basic salary.

Ans.

```
```cpp
#include <iostream.h>

void Cal_Salary (double *bSal)
{
    double da, hra, pf ;
    da = (*bSal * 10)/100;
    hra = (*bSal * 25)/100;
    pf = (*bSal * 10.3)/100;

    *bSal = *bSal + da + hra + pf;
}
int main()
{
double bSal, *tSal;
cout<<"Enter your basic Salary to know Total salary ";\ cin>>bSal;

tSal = &bSal;
Cal_Salary (tSal);
cout<<endl<< *tSal;

return 0;
}
```
```

**Output:**

Enter your Basic Salary to know Total salary 1200

1743.6

Q10. Create a program that accepts marks obtained by the student and displays the result (pass or fail) as well the grade. If marks obtained are more than or equal to 40, the result will be pass, otherwise fail. Grade will be assigned on the basis of following criteria:

| Marks Obtained | Grade |
|---|---|
| Less than 40 | E |
| Between 40 to 50 | D |
| Between 50 to 60 | C |
| Between 60 to 70 | B |
| More than 70 | A |