A special version of std::string for international character sets is std::wstring. Examples are presented later, e.g. in Section 3.18. The complete functional specification of std::string is much longer and contains more calls and syntactic variants than are shown in Table 3.5; so, online references will be helpful.

In this book, we will use std::string and std::wstring quite often. But in some applications, manipulating strings back and forth can lead to inefficiencies. Therefore, SL has the std::stringview class that implements a kind of proxy to the string pattern and in some cases leads to a significant speedup.

More information on C-style text arrays and their manipulating functions is provided in Appendix A.2.6.

# ## 3.7 Using the auto Keyword and decltype for Automatic Type Deduction

In Section 3.1, we discussed the basic built-in C++ objects such as int, double, etc. as well as how they are initialized. We have seen that when assigning an initial value to a variable, their types should match. For example, we wrote the following:

```
```
int x { 0 };
double y { 0.0 };
cout << "x=" << x << endl;
cout << "y=" << y << endl;
```
```

That is, int is initialized with 0, since it is an integer constant; double is initialized with 0.0, since it is a double constant; and so on. On the other hand, from the previous example, we see that by investigating the types of the initializing values, we can automatically deduce the types of the objects x and y. This idea has been incorporated into modern C++ with the help of the auto keyword. By using it, the compiler will automatically determine the type of an object, if possible. For example, the previous code can be rewritten as follows using the auto keyword:

```
```
auto x { 0 };
auto y { 0.0 };
cout << "x=" << x << endl;
cout << "y=" << y << endl;
```
```

The code compiles and prints the same output. Internally, variable x on line [7] is assigned the int type by analyzing the type of its initializer 0, and y on line [9] gets the double type because of its 0.0. We did not gain much from using auto in this example, but in more complex