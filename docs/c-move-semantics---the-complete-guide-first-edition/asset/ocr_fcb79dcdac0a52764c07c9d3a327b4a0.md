# ### 3.3.7 Moving for Members with Disabled Move Semantics

Note that if move semantics is unavailable or has been deleted for a type, this has no influence on the generation of move semantics for classes that have members of this type. The generated default move constructor and assignment operator decide member by member whether to copy or to move it. If a move is not possible (even if the move operation is deleted), a copy is generated (if possible).

For example, assume the following class:

```
```cpp
class Customer {
    ...
public:
    ...
    Customer(const Customer&) = default;          // copying calls enabled
    Customer& operator=(const Customer&) = default; // copying calls enabled
    Customer(Customer&&) = delete;                // moving calls disabled
    Customer& operator=(Customer&&) = delete;     // moving calls disabled
};
```
```

If this class is used by a member in the other class:

```
```cpp
class Invoice {
    std::string id;
    Customer cust;
public:
    ...  // no special member functions
};
```
```

the generated move constructor will move the id string but copy the customer cust:

```
```cpp
Invoice i;
Invoice i1{std::move(i)};   // OK, moves id, copies cust
```
```

# ### 3.3.8 Exact Rules for Generated Special Member Functions

Now we can summarize the new rules for special member functions (when they are generated and how they behave).

As an example, assume we have the following derived class:

```
```cpp
class MyClass : public Base
{
private:
    MyType value;
    ...
};
```
```

The one thing missing here is the noexcept specification, which we introduce later in the chapter about noexcept. However, we will mention the corresponding guarantees here.