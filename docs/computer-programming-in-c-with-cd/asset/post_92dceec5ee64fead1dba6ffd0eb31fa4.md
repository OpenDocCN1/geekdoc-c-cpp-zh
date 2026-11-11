
```cpp
}

cout << sum;

delete [] arr;

return 0;
}
```

**Output:**

```text
Enter number of digits you want to add: 6

Enter number 1: 25

Enter number 2: 50
Enter number 3: 60

Enter number 4: 78

Enter number 5: 98

Enter number 6: 74
Sum of the Numbers you entered is :
```

### Q7. Write a program that accepts a number from user and displays the number with its reciprocal. For getting a reciprocal of the number, using a separate function is must.

Ans.

```cpp
#include <iostream.h>

void reciprocal(double *p1)
{
    *p1=1/(*p1);
}

int main()
{
    double n1;
    cout <<"Enter the number whose reciprocal is required ";
    cin >> n1;
    cout<<"\nThe Number you have entered is: "<<n1<<"\n";
    reciprocal(&n1); // calling function with arguments matching the pointer variables
    cout<<"The reciprocal of the number is: "<<n1;

    return 0;
}
```

**Output:**

```text
Enter the number whose reciprocal is required 12.2356

The Number you have entered is: 12.2356
The reciprocal of the number is: 0.0817287
```

### Q8. Write a program that accepts a string from user and displays the number of vowels in it.

Ans.

```cpp
#include <iostream.h>
#include <string.h>

int vowels(char *str)
{
    int NumVowels = 0;
    for (int i=0; str[i] != '\0'; i++)
    {
        if((str[i] == 'A') || (str[i] == 'E') || (str[i] == 'I') ||
           (str[i] == 'O') || (str[i] == 'U') || (str[i] == 'a') || (str[i] == 'e') ||
           (str[i] == 'i') || (str[i] == 'o') || (str[i] == 'u'))
        {
            NumVowels +=1;
        }
    }
    return NumVowels;
}

int main()
{
    char str[50];
    int NumVowels;
    cout<<"Enter string in which you want to find vowels: ";
    cin>>str;
    NumVowels = vowels(str);
    cout<<endl;
    cout<<"The Number of Vowels in the String are: ";
    cout<<NumVowels;

    return 0;
}
```

**Output:**

```text
Enter string in which you want to find vowels: Dheeraj_Gupta

The Number of Vowels in the String are: 5
```

### Q9. Create a program that accepts basic salary of an employee and then displays his total salary, which includes D.A. 10%, HRA 25%, and PF 10.3% with basic salary.

Ans.

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
    cout<<"Enter your basic Salary to know Total salary ";
    cin>>bSal;

    tSal = &bSal;
    Cal_Salary (tSal);
    cout<<endl<< *tSal;

    return 0;
}
```

**Output:**

```text
Enter your Basic Salary to know Total salary 1200

1743.6
```

### Q10. Create a program that accepts marks obtained by the student and displays the result (pass or fail) as well the grade. If marks obtained are more than or equal to 40, the result will be pass, otherwise fail. Grade will be assigned on the basis of following criteria:

| Marks Obtained | Grade |
|---|---|
| Less than 40 | E |
| Between 40 to 50 | D |
| Between 50 to 60 | C |
| Between 60 to 70 | B |
| More than 70 | A |

Ans.

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
    cout<<"Your Grade is: " << *grade;
    return 0;
}
```

**Output:**

```text
Enter the marks you obtained in the exam: 50
The result of your exam: P
Your Grade is: D
```

### Q11. Create a program that accepts principal amount and number of years from the user. Then it calculates interest @ 8% p.a. and displays it on the screen.

Ans.

```cpp
#include <iostream.h>

void Cal_Int (double *Amount, double years)
{
    double interest ;
    interest = (((*Amount) * years * 8) / 100);
    *Amount = *Amount + interest;
}

int main()
{
    double years, P_Amount, *Amount;
    cout<<"Enter principal Amount: ";
    cin>>P_Amount;

    cout<<endl<<"Enter number of years: ";
    cin>>years;

    Amount = &P_Amount;
    Cal_Int (Amount, years);
    cout<<endl<< *Amount;

    return 0;
}
```

**Output:**

```text
Enter principal Amount: 2500

Enter number of years: 10.25

4550
```

### Q12. Create a tax calculator that accepts employee details and displays the amount of tax to be paid by the employee.

Ans.

```cpp
#include <iostream.h>

char id[10];
char name[30];
char gender;

void Emp_Detail(double *monthSalary)
{
    cout<<"Enter employee id"<<endl;
    cin>>id;
    cout<<"Enter employee name"<<endl;
    cin>>name;
    cout<<"Enter monthly salary"<<endl;
    cin>>*monthSalary;
    cout<<"Enter gender (M/F)"<<endl;
    cin>>gender;
}

void taxCalculate(double *annualSalary, double *taxRate, double *monthSalary, double *taxAmount)
{
    double *as, *tr, *ms, *ta;
    as = annualSalary;
    tr = taxRate;
    ms = monthSalary;
    ta = taxAmount;

    if(gender=='M'||gender=='m')
    {
        *as=(*ms)*12;

        if((*as>150000)&&(*as<=300000))
        {
            *tr=10;
        }
        if((*as>300000)&&(*as<=500000))
        {
            *tr=20;
        }
        if(*as>500000)
        {
            *tr=30;
        }
        *ta=((*as)*(*tr))/100;
    }

    if(gender=='F'||gender=='f')
    {
        *as=(*ms)*12;

        if((*as>180000)&&(*as<=300000))
        {
            *tr=10;
        }
        if((*as>300000)&&(*as<=500000))
        {
            *tr=20;
        }
        if(*as>500000)
        {
            *tr=30;
        }
        *ta=((*as)*(*tr))/100;
    }
}

void display_Detail(double *annualSalary, double *taxRate, double *monthSalary, double *taxAmount)
{
    double *as, *tr, *ms, *ta;
    as = annualSalary;
    tr = taxRate;
    ms = monthSalary;
    ta = taxAmount;

    cout<<"Employee ID : "<<id<<endl;
    cout<<"Name : "<<name<<endl;
    cout<<"Monthly Salary : "<<*ms<<endl;
    cout<<"Annual Salary : "<<*as<<endl;
    cout<<"Tax Rate : "<<*tr<<endl;
    cout<<"Tax Amount : "<<*ta<<endl;
}

void main()
{
    double *monthSalary, *annualSalary, *taxRate, *taxAmount;
    double monthSalary1, annualSalary1, taxRate1, taxAmount1;
    monthSalary1=annualSalary1=taxRate1=taxAmount1=0;

    monthSalary = &monthSalary1;
    annualSalary = &annualSalary1;
    taxRate = &taxRate1;
    taxAmount = &taxAmount1;

    Emp_Detail(monthSalary);
    taxCalculate(annualSalary, taxRate, monthSalary, taxAmount);
    display_Detail(annualSalary, taxRate, monthSalary, taxAmount);
}
```

**Output:**

```text
Enter employee id

KLSI-0029

Enter employee name

Dheeraj

Enter monthly salary
25000
Enter gender (M/F)
M
Employee ID : KSI-T-0029
Name : Dheeraj
Monthly Salary : 25000
Annual Salary : 300000
Tax Rate : 10
Tax Amount : 30000
```

## Summary

In this chapter, you learned to manage memory by using pointers. You are also told to access and change values of an array element by using pointers and pointer arithmetic. Then, you learned to use various operators, such as &, \*, new, and delete, that are required to work with pointers in C++. You also gone through the functions that take pointer variables as their argument, so that the changes made to the variable inside the function body can be reflected outside the function body. Finally, you learned to create functions that can return multiple values in the form of pointer variables.

## Exercises

- **True or False**

  State True or False for the following:

  - Q1. Pointers are variables that can store reference of other variables. **True**
  - Q2. The program using pointers runs slower as compare to program without pointers. **False**
  - Q3. We can directly access the value stored in the other variable, which is pointed by a pointer variable. **True**
  - Q4. We cannot allocate memory to a pointer at run time. **False**
  - Q5. The data type of a pointer variable must be similar to the data type of the variable it points to. **True**
  - Q6. Using dynamic pointers are feasible in terms of memory usage. **True**
  - Q7. We can de-allocate memory of static pointers at run time by using the delete operator. **False**
  - Q8. The & operator is referred as the point to operator. **False**
  - Q9. To declare a pointer, the `*` operator is used. **True**
