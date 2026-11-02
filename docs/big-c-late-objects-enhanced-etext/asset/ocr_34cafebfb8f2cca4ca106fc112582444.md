When the print function is called,
print(x);
the compiler looks at the type of x. If x is a CashRegister object, the first function is called. If x is an Item object, the second function is called. If x is neither, the compiler generates an error.
It is always possible to avoid overloading by giving each function a unique name, such as print_register or print_item. However, we have no choice with constructors. C++ demands that the name of a constructor equal the name of the class. If a class has more than one constructor, then that name must be overloaded.
In addition to name overloading, C++ also supports operator overloading. It is possible to give new meanings to the familiar C++ operators such as +, ==, and <<. This is an advanced technique that we will discuss in Chapter 13.

![](bbox=[0.13, 0.44, 0.22, 0.57])

# Special Topic 9.2

# Initializer Lists

When you construct an object whose data members are themselves objects, those objects are constructed by their class's default constructor. However, if a data member belongs to a class without a default constructor, you need to invoke the data member's constructor explicitly. Here is an example.

This Item class has no default constructor:

```
```cpp
class Item
{
public:
    Item(string item_description, double item_price);
    // No other constructors
    ...
};
```
```

This Order class has a data member of type Item:

```
```cpp
class Order
{
public:
    Order(string customer_name, string item_description, double item_price);
    ...
private:
    Item article;
    string customer;
};
```
```

The Order constructor must call the Item constructor. That is achieved with an initializer list. The initializer list is placed before the opening brace of the constructor. The list starts with a colon and contains names of data members with their construction arguments.

```
```cpp
Order::Order(string customer_name, string item_description, double item_price)
    : article(item_description, item_price)
{
    customer = customer_name;
}
```
```

Initializers are separated by commas. They can also initialize a data member as a copy of a value of the same type. Here is another way of writing the Order constructor:

```
```cpp
Order::Order(string customer_name, string item_description, double item_price)
    : article(item_description, item_price), customer(customer_name)
{
}
```
```