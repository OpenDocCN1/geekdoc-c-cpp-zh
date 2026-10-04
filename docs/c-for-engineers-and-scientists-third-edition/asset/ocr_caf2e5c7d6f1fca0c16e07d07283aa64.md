```
// conversion operator function converting from Date to Intdate class
Date::operator Intdate()    // must return an Intdate object
{
  long temp;
  temp = year * 10000 + month * 100 + day;
  return(Intdate(temp));
}
```

```
// member function to display a Date
void Date::showDate()
{
  cout << setfill('0')
       << setw(2) << month << " /";
       << setw(2) << day << " /";
       << setw(2) << year % 100;
  return;
}
```

```
// class implementation section for Intdate
Intdate::Intdate(long ymd) // constructor
{
  yyyymmd = ymd;
}
```

```
// conversion operator function converting from Intdate to Date class
Intdate::operator Date()    // must return a Date object
{
  int mo, da, yr;
  yr = int(yyyymmd/10000.0);
  mo = int((yyyymmd - yr * 10000.0)/100.0);
  da = int(yyyymmd - yr * 10000.0 - mo * 100.0);
  return(Date(mo,da,yr));
}
```

```
// member function to display an Intdate
void Intdate::showint()
{
  cout << yyyymymd;
  return;
}
```

![](bbox=[0.851, 0.846, 0.879, 0.863])