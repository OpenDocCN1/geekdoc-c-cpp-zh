Therefore, the fact that move semantics is not passed through is a feature, not a bug. If we were to pass move semantics through, we would not be able to use an object that was passed with move semantics twice. For example:

```
    void insertTwice(std::vector<std::string>& coll, std::string& str)
    {
        coll.push_back(str);               // copy str into coll
        coll.push_back(std::move(str));    // move str into coll
    }
```

If all uses of str implicitly had move semantics, the value of str would be moved away with the first push_back() call.

The important lesson to learn here is that a parameter being declared as an rvalue reference restricts what we can pass to this function but behaves just like any other non-const object of this type. We again have to specify when and where we no longer need the value. See the formal discussion *When Rvalues Become Lvalues* for more details.

One additional note: while the print statement of the copy constructor prints the name of the passed customer:

```
    Customer(const Customer& cust)
      : name(cust.name), values(cust.values) {
        std::cout << "COPY " << cust.name << '\n';  // cust.name still there
    }
```

the move constructor cannot use cust.name because in the initialization of the constructor the value might have been moved away. We have to use the member of the new objects instead:

```
    Customer(Customer&& cust)
      : name(std::move(cust.name)), values(std::move(cust.values)) {
        std::cout << "MOVE " << name << '\n';  // have to use name (cust.name moved away)
    }
```

Note that you should always implement the move constructor with a (conditional) noexcept specification to improve the performance of reallocations of a vector of Customers.

# ### 3.2.3 Copy Assignment Operator

The copy assignment operator is implemented as follows:

```
    class Customer {
      private:
        std::string name;       // name of the customer
        std::vector<int> values; // some values of the customer
      public:
        ...
        // copy assignment (assign all members):
        Customer& operator= (const Customer& cust) {
            std::cout << "COPYASSIGN " << cust.name << '\n';
            name = cust.name;
```