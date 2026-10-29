# Display 11.5 Namespace Demonstration (part 1 of 2)

```
1
2 #include <iostream>
3 using namespace std;
4
4 namespace Space1
5 {
6     void greeting( );
7 }
8
8 namespace Space2
9 {
10     void greeting( );
11 }
12
12 void bigGreeting( );
13 int main()
14 {
15     {
16         using namespace Space2;
17         greeting( );
18     }
19
20     {
21         using namespace Space1;
22         greeting( );
23     }
24
25     bigGreeting( );
26
27     return 0;
28 }
29
29 namespace Space1
30 {
31     void greeting()
32     {
33         cout << "Hello from namespace Space1.\n";
34     }
35 }
36
37 namespace Space2
38 {
39     void greeting()
40     {
41         cout << "Greetings from namespace Space2.\n";
42     }
43 }
```

Names in this block use definitions in namespaces Space2, std, and the global namespace.

Names in this block use definitions in namespaces Space1, std, and the global namespace.

Names out here only use definitions in the namespace std and the global namespace.