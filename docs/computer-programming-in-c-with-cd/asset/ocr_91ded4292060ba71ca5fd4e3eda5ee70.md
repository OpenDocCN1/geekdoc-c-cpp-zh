```
```cpp
int ESalary;
public:
    void inputData(int sal, char*name);
    void displayData();
};
void Employee::inputData(int sal, char *name)
{
    strcpy(EName,name);
    ESalary=sal;
}
void Employee::displayData()
{
    cout<<"Name:"<<EName<<endl;
    cout<<"Salary:"<<ESalary<<endl;
}
int main()
{
    int i,j,sal;
    char answer, name[20];
    Employee e[10];       //Creating an array of objects of the Employee class
    j=0;
    for(i=0;i<10;i++)
    {
        cout<<"Initialize employee object (y/n)"<<endl;
        cin>>answer;
        if(answer=='y'||answer=='Y')
        {
            cout<<"Enter employee's name:";
            cin>>name;
            cout<<"Enter employee's salary:";
            cin>>sal;
            e[i].inputData(sal,name);
            j++;
        }
        else
            break;
    }
    cout<<"Employees Details are:"<<endl;
    for(i=0;i<j;i++)
        e[i].displayData();
    return 0;
}
```
```

# Output:

```
Initialize employee object (y/n)
y
Enter employee's name:Neha
```