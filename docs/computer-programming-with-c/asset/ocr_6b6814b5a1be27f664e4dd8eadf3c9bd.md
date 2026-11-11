will perform the addition of members a and b of object d1 and store the result in the variable `res_add()`, which is the private member of object r1. Note that, although a and b are private members of class Data, they can be accessed directly within the function `add()` because Result is declared as a friend class of Data.

Hence, after execution of `add()` function, the state of object r1 will be as shown in Figure 11.34b:

![](bbox=[0.56, 0.212, 0.857, 0.364])

Similarly, the statements

```
r1.sub(d1);
```

and

```
r1.mul(d1);
```

will perform subtraction and multiplication of members a and b by passing object d1 as an argument to the functions `sub()` and `mul()`, respectively. Hence, the final state of object r1 after execution of the functions `add()`, `sub()`, and `mul()` is as shown in the Figure 11.34c.

![](bbox=[0.187, 0.439, 0.74, 0.595])

The following is the full source code to attain the mentioned results:

```
#include<iostream.h>
class Data
{
    private:
    int a,b;
    public:
    void input()
    {
        cout<<"Enter values of members a and b:"<<endl;
        cin>>a>>b;
    }
    friend class Result;
};
class Result
```