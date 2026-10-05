```
};
int main() {
  using namespace lit;
  constexpr Value five{5};
  std::array<Int,"11111"_val> data; // use user-defined literal
  std::cout << data.size() << '\n'; // Output: 5
  std::cout << std::boolalpha;
  std::cout << std::is_literal_type<Value>::value << '\n'; // Output:
true
false
  std::cout << std::is_literal_type<None>::value << '\n'; // Output:
}
```

# Listing 18.21

User-defined literals are especially useful with literal data types.

Doesn't it seem interesting that you can use "11111"_val as a continuous chain parameter? That's because there is a continuous chain of constexpr expressions up to the return val_.

Note that you can only make particularly simple classes with a constexpr constructor into a literal data type. For example, all data fields must also be literal types. A (non-constexpr) destructor prevents such usage.

By the way, you can find out if a type is suitable as a literal data type by using the type trait is_literal_type. In the example, you can see this with None.