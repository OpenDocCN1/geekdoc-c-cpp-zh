```
cout << "ClassB y: " << y << endl;
}

void classB::doubleNum()
{
    classA::doubleNum();
    y = 2 * y;
}

classB::classB(int a, int b)
    : classA(a)
{
    y = b;
}
```

What is the output of the following function main? (4, 12)

```
int main()
{
    classA *ptrA;
    classA objectA(2);

    classB objectB(3, 5);

    ptrA = &objectA;
    ptrA->doubleNum();
    ptrA->print();
    cout << endl;

    ptrA = &objectB;

    ptrA->doubleNum();
    ptrA->print();
    cout << endl;

    return 0;
}
```

35. What is the output of the function main of Exercise 34, if the definition of classA is replaced by the following definition? (13)

```
class classA
{
public:
    virtual void print() const;
    virtual void doubleNum();
    classA(int a = 0);

private:
    int x;
};
```