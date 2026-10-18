# DISPLAY 8.9 Using a Vector

```
1 #include <iostream>
2 #include <vector>
3 using namespace std;
4 
5 int main( )
6 {
7     vector<int> v;
8     cout << "Enter a list of positive numbers.\n"
9         << "Place a negative number at the end.\n";
10 
11     int next;
12     cin >> next;
13     while (next > 0)
14     {
15         v.push_back(next);
16         cout << next << " added. ";
17         cout << "v.size( ) = " <<v.size( ) <<endl;
18         cin >> next;
19     }
20 
21     cout << "You entered:\n";
22     for (unsigned int i = 0; i <v.size( ); i++)
23         cout << v[i] << " ";
24     cout << endl;
25 
26     return 0;
27 }
```

# Sample Dialogue

```
Enter a list of positive numbers.
Place a negative number at the end.
2 4 6 8 -1
2 added. v.size( ) = 1
4 added. v.size( ) = 2
6 added. v.size( ) = 3
8 added. v.size( ) = 4
You entered:
2 4 6 8
```

To set the ith element, for i greater than or equal to 10, you would use push_back.

When you use the constructor with an integer argument, vectors of numbers are initialized to the zero of the number type. If the vector base type is a class type, the default constructor is used for initialization.