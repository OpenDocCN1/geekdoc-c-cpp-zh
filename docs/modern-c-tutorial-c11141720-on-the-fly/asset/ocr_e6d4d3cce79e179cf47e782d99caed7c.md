# 2.6 Object-oriented

# CHAPTER 02: LANGUAGE USABILITY ENHANCEMENTS

```
std::cout << b.value1 << std::endl;
std::cout << b.value2 << std::endl;
}
```

# Inheritance constructor

In traditional C++, constructors need to pass arguments one by one if they need inheritance, which leads to inefficiency. C++11 introduces the concept of inheritance constructors using the keyword: 

```
#include <iostream>
class Base {
public:
  int value1;
  int value2;
  Base() {
    value1 = 1;
  }
  Base(int value) : Base() // delegate delegate() constructor
    value2 = value;
  }
};
class Subclass : public Base {
public:
  using Base::Base; // inheritance constructor
};
int main() {
  Subclass s(3);
  std::cout << s.value1 << std::endl;
  std::cout << s.value2 << std::endl;
}
```

# Explicit virtual function overwrite

In traditional C++, it is often prone to accidentally overloading virtual functions. E.g: 

```
struct Base {
  virtual void foo();
};
struct SubClass: Base {
  void foo();
};
```