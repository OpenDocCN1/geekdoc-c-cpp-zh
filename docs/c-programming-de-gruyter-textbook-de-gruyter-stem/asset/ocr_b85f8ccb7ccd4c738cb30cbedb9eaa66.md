# 7.7 Program Example: Personnel Information Management Program — 309

```
int employee::GetindividualEmpNo()
{ return individualEmpNo; } // get employee number
```

```
int employee::Getgrade()
{ return grade; } // get grade
```

```
float employee::GetAccumPay()
{ return accumPay; } // monthly salary
```

```
technician::technician()
{ hourlyRate=100; } //hourly pay is 100 RMB
```

```
void technician::SetworkHours(int wh)
{ workHours=wh; } //set work hours
```

```
void salesman::pay()
{ accumPay=hourlyRate*CommRate; } //calculate monthly salary by hour
```

```
salesman::salesman()
{ CommRate=0.04; } //commission rate is 4%
```

```
void salesman::Setsales(float sl)
{ sales=sl; } //set sales
```

```
void salesman::pay()
{ accumPay=sales*CommRate; } //salary = sales commissions
```

```
manager::manager()
{ monthlyPay=8000; } //fixed salary is 8000 RMB
```

```
void manager::pay()
{ accumPay=monthlyPay; } //total salary is fixed salary
```

```
salesmanager::salesmanager()
{ monthlyPay=5000;
CommRate=0.005; }
```

```
void salesman::pay()
{ accumPay=monthlyPay+CommRate*sales; } //total salary = fixed salary + sales commission
```