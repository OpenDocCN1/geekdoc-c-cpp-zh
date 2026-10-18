```
```cpp
strcpy(this->name, name);
}

EmployeeMaster* getValuesFromUser()
{
    EmployeeMaster *temp = new EmployeeMaster();
    cout << endl << "Enter user name : ";
    cin >> temp->name;
    cout << endl << "Enter user ID : ";
    cin << temp->id;
    return temp;
}
void displayRecord()
{
    cout << endl << "Name : " << name;
    cout << endl << "ID : " << id << endl;
}
};

void main()
{
    vector <EmployeeMaster*> emp;
    EmployeeMaster *temp = new EmployeeMaster();
    emp.push_back(getValuesFromUser());
    emp[0]->displayRecord();
    delete temp;

    temp = new EmployeeMaster("AlanKay", 3);
    emp.push_back(temp);
    emp[emp.capacity()]->displayRecord();
    emp[emp.size()]->displayRecord();
}
```
```

# 14.2 Identify the error in the following program.

```
```cpp
#include <iostream>
#include <vector>
```
```