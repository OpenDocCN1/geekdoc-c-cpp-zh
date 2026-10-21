```
public :

    string()
    {
        len=0;
        sname= new char [len + 1];
        *sname = '\0';
    }

    string(char s[])
    {
        len=strlen(s);
        sname = new char[len + 1];
        strcpy(sname, s);
    }

    void show()
    {
        cout<<"STRING IS :="<<sname<<endl;
        cout<<"LENGTH :="<<len<<endl;
        delete sname;
    }
};

void main()
{
    string s1,s2;
    clrscr();

    s1 = string("HARI");
    s1.show();

    s2 = string("HARI LIKE C++");
    s2.show();

    getch();
}

OUTPUT :
STRING IS :=HARI
```