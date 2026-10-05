# 18 • Operator Overloading 585

```
float *grd;
int suc; /* This member is added to hold the number of the passed
courses. */
public:
    -Student();
    void show() const;
    int operator+(const Student& s) const;
    friend istream& operator>>(const istream& s const);
    Student& operator=(const Student&) = delete; /* Disable the assignment
operation. */
};

Student::Student()
{
    delete[] grd;
}
int Student::operator+(const Student& s) const
{
    if (suc > s.suc)
        return 1;
    else if (suc < s.suc)
        return 2;
    else
        return 3;
}

void Student::show() const
{
    cout << "\nCode:" << code << '\n';
}

istream& operator>>(istream& in, Student& s)
{
    int i;
    cout << "Enter code: ";
    in >> s.code;
    cout << "Enter number of courses: ";
    in >> s.courses;
    s.grd = new float[s.courses];
    s.suc = 0;
    for(i = 0; i < s.courses; i++)
    {
        cout << "Enter grade: ";
        in >> s.grd[i];
        if(s.grd[i] >= 5)
            s.suc++;
    }
    return in;
}

int main()
{
    int i;
    Student s1, s2;
```