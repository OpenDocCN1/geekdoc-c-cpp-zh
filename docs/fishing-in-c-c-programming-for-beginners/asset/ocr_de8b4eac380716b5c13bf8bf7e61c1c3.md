```
{
    int i=5;
    char ch='c';
    disp(i,ch);
    disp(i);
    disp();
    disp(ch);
}
void disp()
{
    cout<<"In 1"<<endl;
}
void disp(int x)
{
    cout<<"In 2"<<endl;
}
void disp(char c)
{
    cout<<"In 3"<<endl;
}
void disp(int x,char c)
{
    cout<<"In 4"<<endl;
}
Output
In 4
```