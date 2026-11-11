```
```cpp
}
void setData(int x, float y)
{
    acc_no=x;
    bal=y;
}
void displayData()
{
    cout<<"Account Number: "<<acc_no<<endl;
    cout<<"Balance is : "<<bal<<endl;
}
void calc(MoneyTransfer &m, float x);
};
void MoneyTransfer::calc(MoneyTransfer &m, float x)
{
    bal=bal-x; //money deduction from source
    m.bal=m.bal+x; //add money to destination
}

int main()
{
    MoneyTransfer m1,m2,m3;
    int money_trans;
    m1.inputData();
    m2.setData(50);
    m3.setData(80,456.89F);
    cout<<"Account Information"<<endl;
    m1.displayData();
    m2.displayData();
    m3.displayData();
    cout<<"Enter money for transferring from Account3 to Account1:";
    cin>>money_trans;
    m3.calc(m1,money_trans);
    cout<<"Updated Account Information"<<endl;
    m1.displayData();
    m2.displayData();
    m3.displayData();
    return 0;
}
```
```

Output:

```
```text
Enter account number:
10001
Enter the balance:
2000
Account Information
Account Number: 10001
```
```