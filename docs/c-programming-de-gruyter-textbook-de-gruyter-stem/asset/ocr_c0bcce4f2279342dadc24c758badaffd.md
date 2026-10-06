# 10.6 Application — Improving the HR Management Program of a Small Company — 441

```
int i;
for(i=0;i<4;i++)
{
    cout<<"Please input the name of next employee:";
    cin>>namestr;
    vchar[i]->SetName(namestr); //Set name of every employee
    vchar[i]->promote(); //Promote
}
cout<<"Please input the part-time technicians <<<<t1.GetName()<<"'s\nworking hours this week:";
int ww;
cin>>ww;
t1.SetWorkHours(ww); //Set working hours
```

```
cout<<"Please input the sales manager <<<<sm1.GetName()<<"'s total\nsales this month of his department:";
float sl;
cin>>sl;
sm1.Setales(sl); //Set total sales
```

```
cout<<"Please input the salesman <<<<s1.GetName()<<"'s sales this\nmonth:";
cin>>sl;
s1.Setales(sl); //Set sales
```

```
for(i=0;i<4;i++)
{
    vchar[i]->pay(); //Calculate salary
    cout<<vchar[i]->GetName()<<" ID "<<vchar[i]->
GetIndivualEmpNo()<<" Level "
<<vchar[i]->GetGrade()<<", salary this month
<<vchar[i]->GetaccumPay()<<endl;
}
```

Results:

| Please input the name of next employee: Zhang\nPlease input the name of next employee: Wang\nPlease input the name of next employee: Li\nPlease input the name of next employee: Zhao\nPlease input the part-time technicians Wang's working hours this\nweek:40 |