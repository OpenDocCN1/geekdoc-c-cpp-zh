```
//3_10.cpp
#include <iostream>
using namespace std;
void move(char getone, char putone)
{
    cout << getone << "--" << putone << endl;
}
void hanoi(int n, char getone, char two, char three)
{
    move(char getone,char putone);
    if (n==1) move(one,three);
    else
    {
        hanoi(n-1,three,two);
        move(one,three);
        hanoi(n-1,two,one,three);
    }
}
int main()
{
    void hanoi(int n,char one,char two,char three);
    int m;
    cout<<"Enter the number of discs:";
    cin>>m;
    cout<<"the steps to moving """<<m<<"" discs:"<<endl;
    hanoi(m,'A','B','C');
}
```

Running result:
Enter the number of discs:3
the steps to moving 3 discs:
A-->C
A-->B
C-->B
A-->C
B-->A
B-->C
A-->C