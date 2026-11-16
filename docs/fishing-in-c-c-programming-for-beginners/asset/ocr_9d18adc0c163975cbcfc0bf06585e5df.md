```
using namespace std;
class counting
{
    int count;
    public:
    counting() { count=0;}
    int return_value(){return count;}
    void operator++(){++count;}
};
```

```
int main()
{
    counting c1;
    ++c1;
    cout<<c1.return_value()<<endl;
    c1++;
    cout<<c1.return_value()<<endl;
}
```

This program will display an error “Error] no ‘operator++(int)’ declared for postfix ‘++’ [-fpermissive]” .

To overload the postfix operator, we have to pass an argument of integer type, whose value is ignored but it is an indication of the fact that we want to overload the postfix operator.

The syntax for post-increment operator is

```
return_type operator++(int)
{
//Statements
}
```

Consider the following program: