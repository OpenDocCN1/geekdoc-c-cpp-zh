```
```cpp
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
void taxCalculate(double *annualSalary, double *taxRate, double
                  *monthSalary, double *taxAmount)
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
```
```