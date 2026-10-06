# 5.7 Example — Personnel Information Management Program — 193

```
//display information of m1
cout<<number":"<<m1.GetindividualEmpNo()>>
<<"level":"<<m1.Getgrade()<<", this month's pay:
""<<m1.GetaccumPay()>><<endl;
```

```
//display information of t1
cout<<number":"<<t1.GetindividualEmpNo()>>
<<"level":"<<t1.Getgrade()<<", this month's pay:
""<<t1.GetaccumPay()>><<endl;
```

```
//display information of s1
cout<<number":"<<s1.GetindividualEmpNo()>>
<<"level":"<<s1.Getgrade()<<", this month's pay:
""<<s1.GetaccumPay()>><<endl;
}
```

Result:

| Please enter an employee's monthly pay: 8000 |
| Please enter an employee's monthly pay: 4000 |
| Please enter an employee's monthly pay: 7000 |
| Please enter an employee's monthly pay: 1600 |
| Number:1000 level:4, this month's pay: 8000 |
| Number:1001 level:3, this month's pay: 4000 |
| Number:1002 level:3, this month's pay: 7000 |
| Number:1003 level:1, this month's pay: 1600 |

We can find out the result of this example is the same as the result of Example 4.5. However, the use of a static data member in the employee class makes all the objects of the class share this static data. Through this, the employee number can be generated automatically by a constructor every time an object is created.

Also, we have introduced conditional compilation directives in Section 5.6.2. Through the use of conditional compilation directives, we can avoid the compiling error of repeatedly including the employee class. Readers can refer to Section 5.6.2 to add conditional compilation directives into employee.h.