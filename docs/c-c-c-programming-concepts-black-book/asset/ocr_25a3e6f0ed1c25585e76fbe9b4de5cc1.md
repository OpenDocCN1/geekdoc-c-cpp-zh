# # Access Specifier Combinations in C++

Till now, we have come across three types of access specifiers in C++: public, private, and protected. Let's write a program where we combine all the three access specifiers and observe what compiles and runs fine and what gives rise to errors. Although the following program will not compile successfully, but the sole purpose of giving this code snippet is to make the reader aware of common compilation errors due to wrong usage of access specifiers in C++. Listing 14.4 shows the program that combines all the three access specifiers:

Listing 14.4: Showing the Program that Combines all the Three Access Specifiers

```
```cpp
1:/* Inheritance Example Program 3 */
2:#include <iostream.h>
3:using namespace std;
4:
5:class Base {
6:private:
7: int privData;
8:protected:
9: int protData;
10:public:
11:     int pubData;
12:};
13:
14:class Derived1 : public Base {
15:public:
16: void show()
17: {
18:     cout<<privData<<endl;      //Error - Not accessible
19:     cout<<protData<<endl;      //Valid Statement
20:     cout<<pubData<<endl;       //Valid Statement
21: }
22:};
23:
24:class Derived2 : private Base {
25:public:
26: void show()
27: {
28:     cout<<privData<<endl;      //Error - Not accessible
29:     cout<<protData<<endl;      //Valid Statement
30:     cout<<pubData<<endl;       //Valid Statement
31: }
32:};
33:
34:class Derived3 : protected Base {
35:public:
36: void show()
37: {
38:     cout<<privData<<endl;      //Error - Not accessible
39:     cout<<protData<<endl;      //Valid Statement
40:     cout<<pubData<<endl;       //Valid Statement
41: }
42:};
43:
44:int main()
45:{
46: Derived1 der1;
```
```