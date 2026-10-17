```
```cpp
float cost;
public:
void getdata()
{
    cout<<"Enter Seat Section & Cost: "<<endl;
    cin>>ss>>cost;
}
void showdata()
{
    cout<<"Seat : "<<ss<<endl;
    cout<<"Cost: "<<cost<<endl;
}
};
class ring2
{
private:
    float spectators[3];
public:
void getdata()
{
    int i;
    for(i=0;i<3;i++)
    {
        cout<<"\nEnter "<<i+1<<" Section Spectators ";
        cin>> spectators[i];
    }
}
void showdata()
{
    int i;
    for(i=0;i<3;i++)
    {
        cout<<"\n"<<i+1<<" Section Spectators = "<<spectators[i];
    }
}
};

class arena:public ring1,public ring2
{
private :
    int guest;
```
```