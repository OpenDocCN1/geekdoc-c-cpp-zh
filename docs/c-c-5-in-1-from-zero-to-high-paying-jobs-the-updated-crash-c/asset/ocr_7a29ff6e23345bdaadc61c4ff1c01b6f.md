```
class MyClass {
private:
    int data;
public:
    MyClass(int d) : data(d) {}
    friend int accessPrivateData(const MyClass& obj);
};
int accessPrivateData(const MyClass& obj) {
    return obj.data; // Accessing private member through friend function
}
```

# Custom Behavior with Friend Functions:

You can use friend functions to implement behavior that requires access to private members of a class. This can be particularly useful for operations that don't quite fit as member functions.

# Usage of Friend Functions:

In this example, the `accessPrivateData` friend function is used to access the private `data` member of `MyClass`:

```
int main() {
    MyClass obj(42);
    int value = accessPrivateData(obj); // Calls the friend function
    return 0;
}
```

# Summary:

Operator overloading enables you to redefine how operators work with user-defined types, providing custom behavior and making your classes