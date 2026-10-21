```
class demo
{
    int num;

public :

    void input(int x)
    {
        num = x;
    }

    demo copy();

    void show()
    {
        cout << "num=" << num << endl;
    }
};

demo demo ::copy()
{
    demo temp;
    temp.num = num;
    return temp;
}

void main()
{
    clrscr();
    demo d1, d2;

    d1.input(20);
    d2 = d1.copy();

    cout << "Object d1\n";

    d1.show();

    cout << "Object d2\n";
    d2.show();
```