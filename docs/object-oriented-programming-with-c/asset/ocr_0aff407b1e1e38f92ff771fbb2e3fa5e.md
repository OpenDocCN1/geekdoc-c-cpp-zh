```
```cpp
cout << b1 << "\n";
}
};
class B2
{
int b2;
public:
void display();
{
cout << b2 << "\n";
}
};
class D: public B1, public B2
{
// nothing here
};
main()
{
D d;
d.display()
d.B1::display();
d.B2::display();
}
```
```

# Programming Exercises

**8.1** Assume that a bank maintains two kinds of accounts for customers, one called as savings account and the other as current account. The savings account provides compound interest and withdrawal facilities but no cheque book facility. The current account provides cheque book facility but no interest. Current account holders should also maintain a minimum balance and if the balance falls below this level, a service charge is imposed.