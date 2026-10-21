```
class Student
{
    int RollNumber;
    string Name;
public:
    Student(int TempRollNumber, string TempName)
    {
        RollNumber = TempRollNumber;
        Name = TempName;
    }

    bool operator == (Student AnotherStudent) const
    {
        return(RollNumber == AnotherStudent.RollNumber);
    }

    friend ostream & operator <<(ostream & TempOut, Student TempStud)
    {
        TempOut << "Roll number is: " << TempStud.RollNumber << endl;
        TempOut << "Name is: " << TempStud.Name << endl;
    }
};
int main()
{
    vector <Student> vs;
    int IntArray[6];

    for(int i = 0; i < 6; i++)
    {
        IntArray[i] = i;
    }

    Student Lara(1, "Brian Charles Lara");
    Student Beckham(2, "David Beckham");
    Student Steff(3, "Steffi Graf");
    Student Maradona(4, "Diego Maradona");
    Student Tiger(5, "Tiger Woods");
    Student Carl(6, "Carl Lewis");
    vs.push_back(Lara); vs.push_back(Beckham);
    vs.push_back(Steff); vs.push_back(Maradona);
    vs.push_back(Tiger); vs.push_back(Carl);

    // Using find for vector
    vector <Student>::iterator StudentIndex;
    StudentIndex = find(vs.begin(), vs.end(), Maradona);
    cout << *StudentIndex;
    // Using find for integer array
    int *pos = find(IntArray, IntArray + 6, 3);
    cout << *pos << endl;
    // Using find for a list
    list <Student> ls(vs.begin(), vs.end());
    // Creating list from a vector data
    list <Student>::iterator ListIndex;
    ListIndex = find(ls.begin(), ls.end(), Tiger);
    cout << *ListIndex;
    // Using find for a deque
    deque <Student> ds(vs.begin(), vs.end());
```