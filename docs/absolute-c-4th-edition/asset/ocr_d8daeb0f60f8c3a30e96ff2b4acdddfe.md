# Display 4.3 Comparing Argument Mechanisms

```
1 //Illustrates the difference between a call-by-value
2 //parameter and a call-by-reference parameter.
3 #include <iostream>
4 using namespace std;
5 
6 void doStuff(int par1Value, int& par2Ref);
7 //par1Value is a call-by-value formal parameter and
8 //par2Ref is a call-by-reference formal parameter.
9 
10 int main()
11 {
12     int n1, n2;
13 
14     n1 = 1;
15     n2 = 2;
16     doStuff(n1, n2);
17     cout << "n1 after function call = " << n1 << endl;
18     cout << "n2 after function call = " << n2 << endl;
19     return 0;
20 }
21 
22 void doStuff(int par1Value, int& par2Ref)
23 {
24     par1Value = 111;
25     cout << "par1Value in function call = "
26          << par1Value << endl;
27     par2Ref = 222;
28     cout << "par2Ref in function call = "
29          << par2Ref << endl;
30 }
```

# SAMPLE DIALOGUE

par1Value in function call = 111
par2Ref in function call = 222
n1 after function call = 1
n2 after function call = 222

# Pitfall INADVERTENT LOCAL VARIABLES

If you want a function to change the value of a variable, the corresponding formal parameter must be a call-by-reference parameter and therefore must have the ampersand, &, attached to its type. If you carelessly omit the ampersand, the function will have a call-by-value parameter where you meant to have a call-by-reference parameter. When the program is run, you will