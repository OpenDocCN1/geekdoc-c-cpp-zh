```
```cpp
{
cout << “Marks in SUB1 = “ << sub1 << “\n”;
cout << “Marks in SUB2 = “ << sub2 << “\n”;
}
class result : public test // Second level derivation
{
float total; // private by default
public:
void display(void);
};
void result :: display(void)
{
total = sub1 + sub2;
put_number();
put_marks();
cout << “Total = “ << total << “\n”;
}
int main()
{
result student1; // student1 created
student1.get_number(111);
student1.get_marks(75.0, 59.5);
student1.display();
return 0;
}
```
```

The output of Program 8.3 would be:

```
Roll Number: 111
Marks in SUB1 = 75
Marks in SUB2 = 59.5
Total = 134.5
```

# 8.6  Multiple Inheritance