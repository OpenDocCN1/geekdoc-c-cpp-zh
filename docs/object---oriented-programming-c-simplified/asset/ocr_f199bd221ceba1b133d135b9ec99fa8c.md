# # Object-Oriented Programming C++ Simplified

```
public :
emp(int s)
{
sal = s;
}
void operator>(emp temp)
{
if(sal > temp.sal)
cout << "First employee’s salary is higher" << endl;
else
cout << "Second employee’s salary is higher" << endl;
}
void show( )
{
cout << "Salary is " << sal << endl;
}
};

```

```
void main( )
{
clrscr( );
emp e1=emp(12545);
emp e2=emp(13458);
e1.show( );
e2.show( );
e1>e2;
getch( );
}
```

OUTPUT :
Salary is 12545
Salary is 13458
Second employee’s salary is higher

In the program we have overloaded the greater than operator > which compares the salary of the employees. The statement e1>e2 internally interpreted as e1.operator > (e2) i.e., e1 calls the operator function > sends e2 as argument. In the operator function salary of two objects e1 and e2 is compared and result is displayed accordingly.

# ## 8.3 OVERLOADING ASSIGNMENT (=) OPERATOR

We can overload assignment operator if we want to do some extra work other than the simply copy data members from one object to other. The simple copy of two objects can be done as