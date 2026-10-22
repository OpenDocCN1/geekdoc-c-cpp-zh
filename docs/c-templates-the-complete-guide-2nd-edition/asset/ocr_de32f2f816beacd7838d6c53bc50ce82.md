push a string of different size, because it has a different type. For a detailed discussion see Section 7.4 on page 115.

However, when passing arguments of a template type T by value, the parameter *decays*, which is the term for the mechanism to convert a raw array type to the corresponding raw pointer type. That is, the call parameter T of the constructor is deduced to be `char const*` so that the whole class is deduced to be a `Stack<char const*>`.

For this reason, it might be worthwhile to declare the constructor so that the argument is passed by value: [Click here to view code image](#)

```
```cpp
template<typename T>
class Stack {
private:
std::vector<T> elems; // elements
public:
Stack (T elem) // initialize stack with one element by value
: elems({elem}) { // to decay on class tmpl arg deduction
}
…
};
```
```

With this, the following initialization works fine: [Click here to view code image](#)

```
```cpp
Stack stringStack = "bottom"; // Stack<char const*> deduced since C++17
```
```

In this case, however, we should better move the temporary `elem` into the stack to avoid unnecessarily copying it: [Click here to view code image](#)

```
```cpp
template<typename T>
class Stack {
private:
std::vector<T> elems; // elements
public:
Stack (T elem) // initialize stack with one element by value
: elems({std::move(elem)}) {
}
…
};
```
```

# Deduction Guides

Instead of declaring the constructor to be called by value, there is a different solution: Because handling raw pointers in containers is a source of trouble, we should disable automatically deducing raw character pointers for container classes.

You can define specific *deduction guides* to provide additional or fix existing