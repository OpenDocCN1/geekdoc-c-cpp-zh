```
```cpp
{
a=t;
}
};
class C: public P
{
private:
int b;
public:
    C(int x,int y): P(x)
    {
        b=y;
    }
    void display()
    {
        cout<<"Result is "<<a+b;
    }
};
void main()
{
    C o1(50,60);
    o1.display();
}
```
```

![](bbox=[0.124, 0.588, 0.711, 0.667])

To understand the working of constructors, let us understand the given code from the first line of main() function.

The statement

```
C o1(50,60);
```

invokes a constructor with two arguments which is written inside the child class C. Hence, the values 50 and 60 are initialized to the formal arguments x and y created as a part of the constructor definition. Before the child constructor executes further, the parameterized constructor of the parent class is invoked by passing a value of variable x as an argument to the constructor. Hence, the value of the member a of object o1 is now initialized to 50 by the parent constructor. After the execution of the parent constructor completes, the control of execution returns to the child constructor thereby initializing the value of the formal argument y to member b. Hence the value of the member b of the object o1 is 60. Therefore, the function display() prints the result of addition of members a and b as 110 as seen in the output of the code.