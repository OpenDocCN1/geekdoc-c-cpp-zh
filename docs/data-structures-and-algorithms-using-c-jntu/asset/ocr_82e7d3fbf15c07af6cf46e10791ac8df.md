# Program 1.29

```
#include<iostream.h>
#include<conio.h>
void sum(int s)
{
 try
 {
 if(s==0)throw k;
 else
 if(s0)
 throw 'p';
 else if(s<0)throw .3;
 catch(char c)
 {
 cout<<"caught a positive value";
 }
 catch(int i)
 {
 cout<<"caught a null value";
 }
 catch(float f)
 {
 cout<<"caught a negative value";
 }
 }
void main()
{
 cout<<"multiple catches:";
 sum(-5);
 sum(0);
 sum(10);
}
```

# Output

Multiple catches:
Caught a Negative value
Caught a null value
Caught a positive value

In Program 1.29, the function sum() has a try block and there are catch blocks. The first catch block takes the char type object, the second catch block takes integer arguments and the third catch statement takes float type as arguments. The function sum() is called with positive, negative and null values, the argument s takes their values. When s receives a positive value, the throw statement receives a char type exception. When s receives an integer, throws integer type exception similarly when s is negative throws float type. The appropriate catch block is executed when the argument type in it matches with the argument of the throw statement.