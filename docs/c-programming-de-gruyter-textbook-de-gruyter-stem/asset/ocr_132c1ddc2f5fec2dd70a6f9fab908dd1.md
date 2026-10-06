# 254 6 Arrays, Pointers, and Strings

```
{
cout<<"Please input the name of next employee";
cin>>namestr;
emp[i].SetName(namstr); //set name of employee emp[i]
cout<<"Please input the monthly pay of the employee";
cin>>pa;
emp[i]. SetaccumPay(pa); //set monthly pay of employee emp[i]
out<<"Please input promotion grades of the employee";
cin>>grade;
emp[i].promote(grade); //emp[i] promotes
}

//display information
for (i=0; i<4; i++)
{
cout<<emp[i].GetName()<<"number"<<emp[i].GetIndividualEmpNo()
<<"grade is "<<emp[i].GetGrade()<<"grade, current month salary"
<<emp[i].GetaccumPay()<<endl;
}
```

The result is:

Please input the name of next employee: Zhang
Please input the monthly pay of the employee: 8000
Please input promotion grades of the employee: 3
Please input the name of next employee: Wang
Please input the monthly pay of the employee: 4000
Please input promotion grades of the employee: 2
Please input the name of next employee: Li
Please input the monthly pay of the employee: 7000
Please input promotion grades of the employee: 2
Please input the name of next employee: Zhao
Please input the monthly pay of the employee: 1600
Please input promotion grades of the employee: 0
Zhang number 1000 grade is 4, current month salary 4000
Wang number 1001 grade is 3, current month salary 4000
Li number 1002 grade is 3, current month salary 7000
Zhao number 1003 grade is 1, current month salary 1600

In the class employee of this example, we use the character array to store the "name" data member. In order to process the character array that stores the name, we use pointers to pass data. In the main function, we use a temporary array namestr to store