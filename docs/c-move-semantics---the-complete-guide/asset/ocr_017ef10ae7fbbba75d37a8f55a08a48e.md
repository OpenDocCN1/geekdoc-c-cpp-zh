```
values = cust.values;
    return *this;
}
    ...
};
```

Like the automatically generated copy assignment operator, we simply assign all members. The only difference is the print statement at the beginning.

When implementing an assignment operator, you can (and maybe should) check for assignments of an object to itself. However, note that the default assignment operator generated does not do that and see the comments about this when discussing self-assignments with the move assignment operator.

You might also want to declare the assignment operator with reference qualifiers.

# 3.2.4 Move Assignment Operator

The move assignment operator is implemented as follows:

```
class Customer {
private:
    std::string name;        // name of the customer
    std::vector<int> values;  // some values of the customer
public:
    ...
    // move assignment (steal all members):
Customer& operator= (Customer&& cust) {  // noexcept declaration missing
    std::cout << "MOVEASSIGN " << cust.name << '\n';
    name = std::move(cust.name);
    values = std::move(cust.values);
    return *this;
}
};
```

Again, we have to declare the move constructor as a function that takes a non-const rvalue reference. Then in the body, we have to implement how to improve the usual copying by benefiting that we can steal values from the source object.

In this case, we do what the automatically generated move assignment operator would do: we move assign the members in the body instead of copy assigning them. In addition, we add our print statement. Finally, we return the object for further use.

Note that you should usually implement the move assignment operator with a noexcept specification.

You might also want to declare the move assignment operator with reference qualifiers.