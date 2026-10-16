```
void item :: putdata(void)
{
    cout << "Number :" << number << "\n";
    cout << "Cost   :" << cost   << "\n";
}
```

Since these functions do not return any value, their return-type is void. Function arguments are declared using the ANSI prototype.

The member functions have some special characteristics that are often used in the program development. These characteristics are :

+   - Several different classes can use the same function name. The 'membership label' will resolve their scope.
+   - Member functions can access the private data of the class. A non-member function cannot do so. (However, an exception to this rule is a friend function discussed later.)
+   - A member function can call another member function directly, without using the dot operator.

# Inside the Class Definition

Another method of defining a member function is to replace the function declaration by the actual function definition inside the class. For example, we could define the item class as follows:

```
class item
{
    int number;
    float cost;
    public:
        void getdata(int a, float b);      // declaration
        // inline function
        void putdata(void)                // definition inside the class
        {
            cout << number  << "\n";
            cout << cost    << "\n";
        }
};
```

When a function is defined inside a class, it is treated as an inline function. Therefore, all the restrictions and limitations that apply to an inline function are also applicable here. Normally, only small functions are defined inside the class definition.

# 5.5 A C++ Program with Class

All the details discussed so far are implemented in Program 5.1.