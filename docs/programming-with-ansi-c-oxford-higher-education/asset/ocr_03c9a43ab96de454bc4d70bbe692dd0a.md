```
cout << "Designation is " << Designation << "\n";
}
/* Now member functions of the following class can access private variables of this class */
friend CollectionEmp;
/* If forward declaration is not provided, this statement will give an error */
};
class CollectionEmp
{
private:
    employee ColEmp[10];
    /* The collection is in the array form; it can even be a linked list */
    int Index;
public:
    void InitIndex()
    {
        Index = 0;
    }

    bool operator +(employee Emp)
    {
        if(Index < 9)
        {
            ColEmp[Index] = Emp;
            Index++;
            return true;
        }
        else
        {
            return false;
        }
    }

    void ListDeptWise()
    {
        string TempDeptName;
        cout << "Enter the department of the university:";
        cin >> TempDeptName;
        cout << "\n";

        for(int i = 0; i < 10; ++i)
        {
            if(ColEmp[i].DeptName == TempDeptName)
            {
                ColEmp[i].DisplayDetails();
            }
        }
    }
};
void main()
{
    CollectionEmp UniEmpCol;
    UniEmpCol.InitIndex();
    employee UniEmployee[10];

    UniEmployee[1].Init(1,"Lara", "Exam", "Professor");
    UniEmployee[2].Init(2, "Ponting", "Marksheet", "Clerk");
    UniEmployee[3].Init(3, "Laxman", "Accounts", "Head Clerk");
```