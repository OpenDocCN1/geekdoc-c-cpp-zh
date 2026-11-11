```
```cpp
class Student
{
    private:
    int roll_no;
    char name[100];
    int total;
    MarkSheet marks;
    public:
    void inputStud()
    {
        cout<<"Enter Name and Roll Number of the student"<<endl;
        cin>>name>>roll_no;
        /*Also input individual marks*/
        marks.inputMarks();
    }
    void outputStud()
    {
        cout<<"***************************************"<<endl;
        /*Calculate Total marks*/
        total = marks.m1+marks.m2+marks.m3;
        cout<<"Student details are"<<endl;
cout<<"Roll Number="<<roll_no<<"| Name="<<name<<"| Total="
<<total<<endl;
/*print individual marks using MarkSheet object*/
        marks.printMarks();
        cout<<"***************************************"<<endl;
    }
};
void main()
{
    Student s1,s2;
    s1.inputStud();
    s2.inputStud();
    s1.outputStud();
    s2.outputStud();
}
```
```

# Output

```
```text
Enter Name and Roll Number of the student
John 10
Enter Marks m1,m2 and m3
90 85 34
Enter Name and Roll Number of the student
```
```