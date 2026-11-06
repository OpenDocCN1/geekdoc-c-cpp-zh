```
bool operator < (const Employee& first, const Employee& second)
{
    return first.Nickname < second.Nickname;
}
```

```
int main()
{
    map<Employee, Salary> employees;

    Employee emp1("sparky", "123-22-8572");
    Salary sal1(135000, 18);
    employees[emp1] = sal1;

    Employee emp2("buzz", "234-33-5784");
    Salary sal2(150000, 23);
    employees[emp2] = sal2;

    // Now test it out!
    Employee emptest("sparky", "");
    cout << employees[emptest].AnnualRipoff << endl;

    return 0;
}
```

When you run this application, you will see the AnnualRipoff member of the Salary value, where the key is an Employee with the name sparky:

135000

Now notice a couple things about this code. First, to locate the salary for Sparky, we didn't need the Employee instance for Sparky. Instead, we created an instance of Employee and set up the Nickname member without worrying about the SocialSecurityNumber member. Then we retrieved the value by using the bracket notation for map:

```
cout << employees[emptest].AnnualRipoff << endl;
```

Now why did this work? Because the map code uses our less-than function that we provided. And in that function, we compared only the Nickname members, not the SocialSecurityNumber member. We could, however, change things around a bit. Instead of comparing the Nickname members, we could compare the SocialSecurityNumber members. We could change the less-than function like so:

```
bool operator < (const Employee& first,
const Employee& second)
{
    return first.SocialSecurityNumber <
        second.SocialSecurityNumber;
}
```

Book IV
Chapter 6
Programming with
the Standard Library