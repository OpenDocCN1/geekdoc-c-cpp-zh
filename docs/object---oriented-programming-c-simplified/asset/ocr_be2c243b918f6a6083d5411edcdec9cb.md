```
void input(char s[], int a, float f)
{
    strcpy(name, s);
    age = a;
    sal = f;
}
void show()
{
    cout << "Name =" << name << endl;
    cout << "Age =" << age << endl;
    cout << "Salary =" << sal << endl;
    cout << "Address :=" << addr.hno << "," << addr.street << endl;
    cout << "\t" << addr.city << "," << addr.state << endl;
}
};

void main()
{
    person p;

    clrscr();

    p.input("HARI",24,15000);
    strcpy(p.addr.hno,"s17/127");
    strcpy(p.addr.street,"23");
    strcpy(p.addr.city,"Varanasi");
    strcpy(p.addr.state,"UP");

    cout << "\n\t PERSON DETAILS\n\n";

    p.show();
    getch();
}
```

# OUTPUT :

PERSON DETAILS

Name = HARI
Age = 24
Salary = 15000