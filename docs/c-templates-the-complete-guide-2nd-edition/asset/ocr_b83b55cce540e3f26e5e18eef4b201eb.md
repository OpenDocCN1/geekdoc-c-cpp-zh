```
int main()
{
    // provide our own hash function:
    struct MyCustomerHash {
        // NOTE: missing const is only an error with g++ and clang:
        std::size_t operator() (Customer const& c) {
            return std::hash<std::string>()(c.getName());
        }
    };

    // and use it for a hash table of Customers:
    std::unordered_set<Customer,MyCustomerHash> coll;
    ...
}
```