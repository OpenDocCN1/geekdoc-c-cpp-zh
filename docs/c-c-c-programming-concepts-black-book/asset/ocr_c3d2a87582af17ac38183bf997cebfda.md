Similarly, other binary operator, such as -, +, or *, can also be overloaded. Let's overload the ++ operator in C++ for the TickCounter class, as follows:

```
    1:/* Operator Overloading Example Program 6 */
    2:#include <iostream.h>
    3:using namespace std;
    4:
    5:class TickCounter {
    6:   int count;
    7:public:
    8: TickCounter()
    9: {
    10:       count=0;
    11:   }
    12:   TickCounter(int cnt)
    13:   {
    14:       count = cnt;
    15:   }
    16: int getCount ()
    17: {
    18:       return this->count;
    19: }
    20: void operator += (TickCounter obj)
    21: {
    22:       count = count + obj.count;
    23:   }
    24:};
    25:
    26:int main()
    27:{
    28:   TickCounter obj1(100);
    29:   TickCounter obj2(450);
    30:
    31:   cout<<"The value of Obj1 = "<<obj1.getCount()<<endl;
    32:   cout<<"The value of Obj2 = "<<obj2.getCount()<<endl;
    33:
    34:   obj1 += obj2;
    35:
    36:   cout<<"\nThe value of Obj1 = "<<obj1.getCount()<<endl;
    37:   cout<<"The value of Obj2 = "<<obj2.getCount()<<endl;
    38:
    39:   return 0;
    40:}
```

In the preceding program, we have overloaded the ++ operator over the TickCounter class to show how it is implemented to work on user-defined class objects. When we overload this kind of operator, we just need to keep in mind that we are simply combining an assignment operator with the addition operator. Following is the output of the preceding program:

```
    The value of obj1 = 100
    The value of obj2 = 450
    The value of obj1 = 550
    The value of obj2 = 450
```