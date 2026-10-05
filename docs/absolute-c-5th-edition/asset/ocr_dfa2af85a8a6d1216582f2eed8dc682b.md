# Parameters 157

> TIP: (continued)

is a local variable) is set to 111 in the function body, and this value is output to the screen. However, the value of the argument n1 is not changed. As shown in the sample dialogue, n1 has retained its value of 1.
On the other hand, par2Ref is a call-by-reference parameter. When the function is called, the argument n2 (not just its value) is substituted for the formal parameter par2Ref. When the following code is executed,

```
par2Ref = 222;
```

it is the same as if the following were executed:

```
n2 = 222;
```

Thus, the value of the variable n2 is changed when the function body is executed, so the dialogue shows, the value of n2 is changed from 2 to 222 by the function call. If you keep in mind the lesson of Display 4.3, it is easy to decide which mechanism to use. If you want a function to change the value of a variable, the corresponding formal parameter must be a call-by-reference parameter and must be marked with the ampersand sign, &. In all other cases, you can use a call-by-value

![](bbox=[0.121, 0.473, 0.143, 0.493])

# Display 4.3 Comparing Mechanisms (part 1 of 2)

```
1 //Illustrates the difference between a call-by-value
2 //parameter and a call-by-reference parameter.
3 #include <iostream>
4 using namespace std;

5 void doStuff(int parValue, int &par2Ref);
6 //parValue is a call-by-value formal parameter
7 //par2Ref is a call-by-reference formal parameter.

8 int main ()
9 {
10 int n1, n2;
11 n1 = 1;
12 n2 = 2;
13 doStuff(n1, n2);
14 cout << "n1" after function call = " << n1 << endl;
15 cout << "n2" after function call = " << n2 << endl;
16 return 0;
17 }\18
```

```
19 void doStuff(int parValue, int &par2Ref)
20 {
21 parValue = 111;
```

(continued)