```
{
//Statements
}
```

Consider the following program:

```
#include<iostream>
using namespace std;
class student
{
    public:
    char name[50];
    char section;
    int roll;
    void read_data();
};
void display_data(student);
void student::read_data()
{
    cout<<"Enter the name\n";
    cin.getline(name,50);
    cout<<"Enter the section\n";
    cin>>section;
    cout<<"Enter the roll number\n";
    cin>>roll;
}
int main()
{
    class student s1;
    s1.read_data();
    display_data(s1);
}
void display_data(student x)
{
    cout<<"Name of the student is: ";
    cout<<x.name;
    cout<<"\nThe section of the student is: ";
    cout<<x.section;
    cout<<"\nThe roll number of the student is: ";
    cout<<x.roll;
}
```

# Output

Enter the name
Aman Kumar Jha
Enter the section
D
Enter the roll number