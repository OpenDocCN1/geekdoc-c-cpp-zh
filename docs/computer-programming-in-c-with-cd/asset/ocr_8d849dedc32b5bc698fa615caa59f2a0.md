```
```cpp
{
}
Addition(int a, int b)
{
    x=a;
    y=b;
    result=x+y;
}
Addition(float p, float q)
{
    fl1=p;
    fl2=q;
    result=fl1+fl2;
}
Addition(float a, int b)
{
    fl1=a;
    x=b;
    result=fl1+x;
}
void display()
{
    cout<<"After addition: "<<result<<endl;
}
};

int main()
{
    Addition a1, a2, a3;
    float var1, var2;
    int num1,num2;
    char ch;
    cout<<"tadd your data"<<endl;
    cout<<"Enter your choice"<<endl;
    cout<<" 1: Add two numbers"<<endl;
    cout<<" 2: Add two numbers in decimals"<<endl;
    cout<<" 3: Add one decimal and one number"<<endl;
    cin>>ch;
    cout<<"Enter your data"<<endl;
    if(ch=='1')
    {
        cin>>num1>>num2;
        a1=Addition(num1,num2);
        cout<<"Object 1 calling"<<endl;
        a1.display();
    }

    else if(ch=='2')
```
```