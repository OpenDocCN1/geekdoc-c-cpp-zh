```
~~~cpp
{
  int a,b;
  cout<<"Enter a = ";
  cin>>a;
  cout<<"Enter b = ";
  cin>>b;
  TestException obj(a,b);
  std::cout<<"Trying to divide"<<"\n";
  int quotient = obj.divide();
  if (quotient==-1)
    throw quotient;
  else
    cout<<"quotient="<<quotient;
}
catch(int quotient)
{
  std::cout<<"caught an exception"<<quotient;
}
};
~~~
```

+   - (a) Trying to divide
+       a=100
+       b=100
+       a/b=1
+       quotient=1
+   - (b) Trying to divide
+       a=100
+       b=100
+       a/b=-1
+       caught an exception-1
+   - (c) Trying to divide
+       a=100
+       b=100
+       a/b=1
+       caught an exception1
+   - (d) None of the above

Answer: (a)

12. Predict the output of the following code,
given a=100, b=100

```
~~~cpp
#include <iostream>
using namespace std;
int main (void)
{
  try
  {
    int a,b;
    cout<<"Enter a = ";
    cin>>a;
    cout<<"Enter b = ";
    cin>>b;
    std::cout<<"Trying to divide"<<"\n";
    int quotient = a/b;
    if (quotient==-1)
    {
      throw quotient;
      cout<<"after throw";
    }
    else
      cout<<"quotient="<<quotient;
  }
  catch(int quotient)
  {
    std::cout<<"after catch"<<quotient;
  }
};
~~~
```

+   - (a) Trying to divide
+       after throw
+       after catch
+   - (b) Trying to divide
+       after catch
+   - (c) after catch
+       after throw
+   - (d) after throw
+       after catch

Answer: (a) The statements after catch will not be executed, they remain unreachable code.