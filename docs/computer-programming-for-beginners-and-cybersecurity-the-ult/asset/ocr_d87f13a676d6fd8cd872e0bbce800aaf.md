```
cout<<"ID "<<ID<<endl;

cout<<"Name "<<Name;

}
// Note that we have defined the city property as private
private:
    string city;
};
class Student:public Person {
public:
    void Display()
    {
        cout<<"Student ID "<<ID<<endl;
        cout<<"Student Name "<<Name<<endl ;
    }
};
int main () {
    Student stud1;
    stud1.ID=1;
    stud1.Name="John";
    stud1.Display();
    return 0;
}
```

With this program, the output is as follows: