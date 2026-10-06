8.6 Program Instance: Improvement on Staff Information Management System — 347

```
for(i=0;i<4;i++)
{
    cout<<"Please input next employee's name";
    cin>>namestr;
    emp[i]->SetName(namestr);   //set name for each employee
    emp[i]->promote();
    //promote, access derived-class function by base-class pointer
}
cout<<"Please input part-time technician"<<t1.GetName()<<"current
work hours:"
intww;
int ww;
cin>>ww;
t1.SetWorkHours(ww);   //set work hours

cout<<"Please input sales manager"<<sm1.GetName()<<"current sales
in his department:"
float sl;
cin>>sl;
sm1.Setsales(sl);   //set sales
cout<<"Please input salesman"<<s1.GetName()<<"current sales:"
cin>>sl;
s1.Setsales(sl);   //set sales
for(i=0;i<4;i++)
{
    emp[i]->pay();
    //calculate salary, access derived-class function by base-class
    //pointer
    cout<<emp[i]->GetName()<<"employee number:"<<emp[i]->
    <<GetIndividualEmpNo()
    <<"grade is"<<emp[i]->GetGrade()<<",salary is"<<emp[i]->
    <<GetacacumpPay()<<endl;
n}
```

The execution result is:

```
Please input next employee's name:Zhang
Please input next employee's name:Wang
Please input next employee's name:Li
Please input next employee's name:Zhao
Please input part-time technician Wang current work hours:40
Please input sales manager Li current sales in his department:400000
```