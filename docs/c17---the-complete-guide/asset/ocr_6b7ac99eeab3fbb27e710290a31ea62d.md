# 24.3 Using Searcher Predicates

When using searchers, you can use predicates, which might be necessary for two reasons:

+   1. You want to define your own way of comparing two elements.

+   2. You want to provide a hash function, which is necessary for the Boyer-Moore(-Horspool) searchers.

You have to provide the predicates as additional arguments to the constructor of the searchers. For example, here we are searching for a substring case-insensitively:

```
std::boyer_moore_searcher bmic{substr.begin(), substr.end(),
    [](char c){
        return std::hash<char>{}(std::toupper(c));
    },
    [](char c1, char c2){
        return std::toupper(c1)==std::toupper(c2);
    }
};
auto begend = bmic(sub.begin(), sub.end());
```

Do not forget to call toupper() before you hash the value, because otherwise you violate the requirement that the hash value must be the same for all values, where operator== yields true.

And here, if we have a class Customer defined as follows:

```
class Customer {
    ...
public:
    Customer() = default;
    std::string getID() const {
        return id;
    }
    friend bool operator== (const Customer& c1, const Customer& c2) {
        return c1.id == c2.id;
    }
};
```

we can search for a subsequence of customers in a vector of customers as follows:

```
std::vector<Customer> customers;
...
std::vector<Customer> sub{...};
...
std::boyer_moore_searcher bmcust(sub.begin(), sub.end(),
    [](const Customer& c) {
        return std::hash<std::string>{}(c.getID());
    });
auto pos = bmcust(customers.begin(), customers.end());
if (pos.first != customers.end()) {
    ...
}
```