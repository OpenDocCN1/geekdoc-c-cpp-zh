```
char MyName[];
cout << "a:" << a << endl;
cout << "b:" << b << endl;
cout << "Your name please:";
cin >> MyName;
cout << "Welcome dear" << MyName << "to the world
of C++!";
}
Output:
a: 110
b: 0.11
Your name please: Saurabh
Welcome dear Saurabh to the world of C++!
```

The keyword cin is used for input in C++. The operator >> is used to separate the variables being input or output. A whitespace is used to separate items corresponding to different variables on the standard input device. The shift right operator >> is overloaded by C++ for this purpose. It is also called input operator or extraction operator. Program Code A.3 uses cin and cout for accepting two integers from the user and then displaying the sum of the two input numbers.

```
//A sample C++ program for illustrating cin and cout
#include<iostream.h>
main()
{
int a, b;
cout << "Enter values of a & b:";
cin >> a >> b;
cout << a << " + " << b << " = " << a + b;
}
Output:
Enter values of a & b: 5 6
5 + 6 = 11
```

An advantage of I/O in C++ is that it is format-free, that is, the programmer is not required to use formatting symbols to specify the type and order of items being input or output. Similar to other C++ operators, I/O operators can also be overloaded.