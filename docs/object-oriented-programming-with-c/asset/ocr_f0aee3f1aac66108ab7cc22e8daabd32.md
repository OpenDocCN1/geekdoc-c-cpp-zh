```
```
void show_a(void);
};
class D : public B// public derivation
{
int c;
public:
void mul(void);
void display(void);
};
//--------------------------------------------------
void B :: set_ab(void)
{
 a = 5; b = 10;
}
int B :: get_a()
{
return a;
}
void B :: show_a()
{
cout << "a = " << a << "\n";
}
void D :: mul()
{
c = b * get_a();
}
void D :: display()
{
cout << "a = " << get_a() << "\n";
cout << "b = " << b << "\n";
cout << "c = " << c << "\n";
}
//--------------------------------------------------
int main()
{
```
```