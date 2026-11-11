```
```cpp
};
int Sample::count=0;
int main()
{
cout<<"Before instance of the class is created"<<endl;
Sample::dis1();
Sample a,b,c;
cout<<"After instances of the class is created"<<endl;
a.dis2();
b.dis2();
c.dis2();
Sample::dis1();
return 0;
}
```
```

Output:

```
```text
Before instance of the class is created
Static Function calling
The value stored in static variable is:0
After instances of the class is created
Normal Function calling
The value stored in normal variable is:1
The value stored in static variable is:3
Normal Function calling
The value stored in normal variable is:1
The value stored in static variable is:3
Normal Function calling
The value stored in normal variable is:1
The value stored in static variable is:3
Static Function calling
The value stored in static variable is:3
```
```

In Listing 37, the static method, dis1(), is called directly by using the class name (Sample) and the scope resolution (::) operator in the main() function.

> Write a note on Static members of classes and objects (Mumbai University, December 2007)

After explaining how to create and use static members in a class, let's describe the concept of overloading in C++.