Ans.

```
```cpp
#include <iostream.h>
char* get_result (int marks)
{
    char *result;
    if (marks < 40)
    {
        result = "F";
    }
    else
    {
        result = "P";
    }
    return result;
}
char* get_grade (int marks)
{
    char *grade;
    if (marks < 40)
    {
        grade = "E";
    }
    if ((marks >=40) && (marks <=50))
    {
        grade = "D";
    }
    if ((marks >50) && (marks <=60))
    {
        grade = "C";
    }
    if ((marks >60) && (marks <=70))
    {
        grade = "B";
    }
    if (marks > 70)
    {
        grade = "A";
    }
    return grade;
}
int main ()
{
    int marks;
    char *result, *grade;
    cout<<"Enter the marks you obtained in the exam: ";
    cin>> marks;
    result = get_result (marks);
    grade = get_grade (marks);
    cout<<"The result of your exam: " << *result<<endl;
```
```