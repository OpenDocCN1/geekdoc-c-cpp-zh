during the compilation phase, even though the ‘+’ operator is applied to a user-defined object. This is because of the operator function definition in the class body. As soon as the compiler encounters the operator function definition, it first checks the data type of the operand. If the operand is of built-in data type, the compiler knows what to do, but when ‘+’ is applied over an object, the compiler searches the class definition to see whether this operator has been overloaded as a class member function. If not, then the compiler issues an error and fails the compilation process; otherwise, it does the job as specified in the definition of ‘+’. In the preceding program, we have incremented obj1 only once and obj2 twice. To see whether this operation has been succeeded, the values are again printed in line numbers 33 and 34.

Following is the output of the preceding program:

```
The value of obj1 = 0
The value of obj2 = 0
The value of obj1 = 1
The value of obj2 = 2
```

Now, in the preceding program, we have kept the return type of the operator function as void. However, we can experiment in the same program with return types other than void. Let’s write the same program, but the operator function will return an object instead of void, given as follows:

```
1: /* Operator Overloading Example Program 2 */
2: #include <iostream>
3: using namespace std;
4:
5: class TickCounter {
6:     int count;
7: public:
8:     TickCounter()
9:     {
10:        count=0;
11:    }
12:    int getCount()
13:    {
14:        return this->count;
15:    }
16:    TickCounter operator ++()
17:    {
18:        ++count;
19:        TickCounter tempObj;
20:        tempObj.count = count;
21:        return tempObj;
22:    }
23: };
24:
25: int main()
26: {
27:    TickCounter obj1, obj2;
28:
29:    cout<<"The value of obj1 = "<<obj1.getCount()<<endl;
30:    cout<<"The value of obj2 = "<<obj2.getCount()<<endl;
31:
32:    ++obj1;
33:    obj2 = ++obj1;
34:
35:    cout<<"\nthe value of obj1 = "<<obj1.getCount()<<endl;
36:    cout<<"The value of obj2 = "<<obj2.getCount()<<endl;
37: }
```