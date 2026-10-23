```
stacks<int> s1;
clrscr();
if(s1.isEmpty())
cout<<"Stack is empty"<<endl;
else
cout<<"Stack is not empty";
s1.push(10);
s1.push(5);
//s1.push(7);
s1.push(14);
cout<<"Total    number    of    elements    in    stack    are:"<<s1.count_elements()<<endl;
s1.push(90);
//s1.push(299);
cout<<" Element(s) in the stack are:"<<endl;
s1.display();
n=s1.pop();
cout<<" Element pop is "<<n<<endl;
getch();
return 0;
}
```

# 5.5.2 Dynamic stack using template

```
#include<iostream.h>
#include<conio.h>
//using namespace std;
const int size=5;
template <class t>
class stacks
{
    t stack[size];
    int top;
    public:
        stacks()
        {
```