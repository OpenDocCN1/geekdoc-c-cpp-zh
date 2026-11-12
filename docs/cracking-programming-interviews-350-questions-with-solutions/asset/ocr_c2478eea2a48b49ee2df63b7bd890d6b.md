+   * if the member function is declared volatile, the type of this is volatile X*, and
+   * if the member function is declared const volatile, the type of this is const volatile X*.

Thus in a const member function, the object for which the function is called is accessed through a const access path.

# ### *** Question 174 scope of static member

What is output of the program below?

Program 13.1: scope of static member

```
```cpp
1 #include <iostream>
2
3 int g()
4 {
5     return 1;
6 }
7
8 struct X
9 {
10    static int g()
11    {
12        return 10;
13    }
14 };
15
16 struct Y : X
17 {
18    static int i;
19 };
20
21 int Y::i = g();
22
23 int main()
24 {
25    std::cout << Y::i << std::endl;
26 }
```
```

# ### Solution of Question 174

It prints 10. Because the code int Y::i = g(); is equivalent int Y::i = Y::g();.

# ### *** Question 175 static member function

What are the properties of a static member function?

# ### Solution of Question 175

+   * A static member function does not have a this pointer.