```
```cpp
};
class sprint : public hyrdrolic
{
    protected :
        int maxLoad;
    public:
        void getdata()
        {
            hyrdrolic :: getdata();
            cout<<"Enter max goods load: ";
            cin>>maxLoad;
        }
        void showdata()
        {
            hyrdrolic :: showdata();
            cout<<"GMotor Capacity = "<<maxLoad<<endl;;
        }

};
int main()
{
    fuel f1;
    race r1;
    cout<<"Enter details of vehicle: "<<endl;
    f1.getdata();
    r1.getdata();
    cout<<"Vehicle Specifications are: "<<endl;
    f1.showdata();
    r1.showdata();
}
```
```

# Output:

```
```text
Enter details of vehicle:
Enter team name
Redbull
Enter light motor number: 27789
Enter Gear motor capacity: 4900
Enter team name
Redbull
Enter passenger capacity: 1
Vehicle Specifications are:
Team Name : Redbull
```
```