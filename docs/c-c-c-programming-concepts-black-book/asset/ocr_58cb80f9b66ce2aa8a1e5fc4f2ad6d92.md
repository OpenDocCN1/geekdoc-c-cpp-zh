this situation. Then, how can we write statements that have non-member data types to the left of the operator?
A **friend** operator function can help us out in this dilemma. Let’s rewrite the preceding program again using friend operator functions:

```
```cpp
1:/* Operator Overloading Example Program 11 */
2:#include <iostream>
3:using namespace std;
4:
5:class Counter {
6:    int count;
7:public:
8:    Counter() {
9:        count = 0;
10:    }
11:    Counter (int cnt) {
12:        count = cnt;
13:    }
14:    void show() {
15:        cout<<"Count = "<<count<<endl;
16:    }
17:    friend Counter operator + (Counter obj1, Counter obj2);
18:};
19:
20:Counter operator + (Counter obj1, Counter obj2) {
21:    int tempcnt = 0;
22:    tempcnt = obj1.count + obj2.count;
23:    return (tempcnt);
24:}
25:
26:int main ()
27:{
28:    Counter obj1(51);
29:    Counter obj2(15);
30:    Counter obj3;
31:
32:    obj3 = obj1 + obj2;
33:
34:    obj1.show();
35:    obj2.show();
36:    obj3.show();
37:
38:    obj3 = obj1 + 10;      /* This is valid */
39:    obj3.show();
40:
41:    obj3 = 10 + obj2;      /* This is valid now using friend fn */
42:    obj3.show();
43:
44:    return 0;
45:}
```
```

In the preceding program, the overloaded ‘+’ operator is made into a friend operator function, as follows:

```
```cpp
friend Counter operator + (Counter obj1, Counter obj2);
```
```

Notice that, while the overloaded ‘+’ operator took one argument as a member function, it takes two arguments as a friend function. In a member function, one of the objects on which the ‘+’ operator operates is the object of which it is a member, and the second is an argument. In a friend operator function, both objects