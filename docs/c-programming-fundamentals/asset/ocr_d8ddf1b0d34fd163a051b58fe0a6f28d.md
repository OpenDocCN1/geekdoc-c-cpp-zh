```
```cpp
{
    f1Car :: getdata();
    cout<<"Enter light motor number: ";
    cin>>LmotNo;
}
void showdata()
{
    f1Car:: showdata();
    cout<<"LMotor No = "<<LmotrNo<<endl;
}

};
class hydrolic : public f1Car
{
protected:
    float price;
public :
    void getdata()
    {
        f1Car :: getdata();
        cout<<"Enter heavy motor price: ";
        cin>>price;
    }
    void showdata()
    {
        f1Car :: showdata();
        cout<<"HMotor Price = "<<price<<Endl;
    }

};
class fuel: public engine
{
protected :
    int capacity;
public:
    void getdata()
    {
        engine :: getdata();
        cout<<"Enter Gear motor capacity: ";
        cin>>capacity;
    }
```

```