```
```cpp
class city
{
protected:
    char *name;
    int len;
public:
    city( )
    {
        len = 0;
        name = new char[len+1];
    }

    void getname(void)
    {
        char *s;
        s = new char[30];
        cout << “Enter city name:”;
        cin >> s;
        len = strlen(s);
        name = new char[len + 1];
        strcpy(name, s);
    }

    void printname(void)
    {
        cout << name << “\n”;
```
```