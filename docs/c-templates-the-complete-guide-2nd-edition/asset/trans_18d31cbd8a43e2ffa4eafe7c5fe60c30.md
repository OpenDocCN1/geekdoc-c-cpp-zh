

```cpp
template<typename T, auto Maxsize>
void Stack<T,Maxsize>::pop ()
{
    assert(!elems.empty());
    --numElems;            // decrement number of elements
}

template<typename T, auto Maxsize>
T const& Stack<T,Maxsize>::top () const
{
    assert(!elems.empty());
    return elems[numElems-1];  // return last element
}
```

```cpp
template<typename T, auto Maxsize>
class Stack {
    ...
};
```

```cpp
std::array<T,Maxsize> elems;    // elements
```

```cpp
using size_type = decltype(Maxsize);
```

```cpp
size_type size() const {    // return current number of elements
    return numElems;
}
```

```cpp
auto size() const {                 // return current number of elements
    return numElems;
}
```

### basics/stackauto.cpp

```cpp
#include <iostream>
#include <string>
#include "stackauto.hpp"

int main()
{
    Stack<int,20u>      int20Stack;      // stack of up to 20 ints
    Stack<std::string,40> stringStack;    // stack of up to 40 strings

    // manipulate stack of up to 20 ints
    int20Stack.push(7);
    std::cout << int20Stack.top() << '\n';
    auto size1 = int20Stack.size();

    // manipulate stack of up to 40 strings
    stringStack.push("hello");
    std::cout << stringStack.top() << '\n';
    auto size2 = stringStack.size();

    if (!std::is_same_v<decltype(size1), decltype(size2)>) {
        std::cout << "size types differ" << '\n';
    }
}
```

```cpp
Stack<int,20> int20Stack;    // stack of up to 20 ints
```

```cpp
Stack<std::string,40> stringStack;    // stack of up to 40 strings
```

```cpp
auto size1 = int20Stack.size();
...
auto size2 = stringStack.size();
```

```cpp
if (!std::is_same<decltype(size1), decltype(size2)>::value) {
    std::cout << "size types differ" << '\n';
}
```

```cpp
if (!std::is_same_v<decltype(size1), decltype(size2)>) {
    std::cout << "size types differ" << '\n';
}
```

```cpp
Stack<int,3.14> sd;  // ERROR: Floating-point nontype argument
```

### basics/message.cpp

```cpp
#include <iostream>

template<auto T>      // take value of any possible nontype parameter (since C++17)
class Message {
    public:
        void print() {
            std::cout << T << '\n';
        }
};

int main()
{
    Message<42> msg1;
    msg1.print();           // initialize with int 42 and print that value

    static char const s[] = "hello";
    Message<s> msg2;        // initialize with char const[6] "hello"
    msg2.print();           // and print that value
}
```

### basics/varprint1.hpp

```cpp
#include <iostream>

void print ()
{
}

template<typename T, typename... Types>
void print (T firstArg, Types... args)
{
    std::cout << firstArg << '\n';  // print first argument
    print(args...);                 // call print() for remaining arguments
}
```

```cpp
void print (T firstArg, Types... args)
```

```text
7.5
hello
world
```

```cpp
print<double, char const*, std::string> (7.5, "hello", s);
```

```cpp
print<char const*, std::string> ("hello", s);
```

```cpp
print<std::string> (s);
```

### basics/varprint2.hpp

```cpp
#include <iostream>

template<typename T>
void print (T arg)
{
    std::cout << arg << '\n';  // print passed argument
}

template<typename T, typename... Types>
void print (T firstArg, Types... args)
{
    print(firstArg);             // call print() for the first argument
    print(args...);              // call print() for remaining arguments
}
```

```cpp
template<typename... T>
auto foldSum (T... s) {
    return (... + s);  //((s1 + s2) + s3)...
}
```

### basics/foldtraverse.cpp

```cpp
// define binary tree structure and traverse helpers:
struct Node {
  int value;
  Node* left;
  Node* right;
  Node(int i=0) : value(i), left(nullptr), right(nullptr) {
  }
  ...
};
auto left = &Node::left;
auto right = &Node::right;

// traverse tree, using fold expression:
template<typename T, typename... TP>
Node* traverse (T np, TP... paths) {
  return (np ->* ... ->* paths);    // np ->* paths1 ->* paths2 ...
}

int main()
{
  // init binary tree structure:
  Node* root = new Node{0};
  root->left = new Node{1};
  root->left->right = new Node{2};
  ...
  // traverse binary tree:
  Node* node = traverse(root, left, right);
  ...
}
```

```cpp
template<typename... Types>
void print (Types const&... args)
{
    (std::cout << ... << args) << '\n';
}
```

### basics/addspace.hpp

```cpp
template<typename T>
class AddSpace
{
    private:
        T const& ref;                      // refer to argument passed in constructor
    public:
        AddSpace(T const& r): ref(r) {
        }
        friend std::ostream& operator<< (std::ostream& os, AddSpace<T> s) {
            return os << s.ref << ' ';     // output passed argument and a space
        }
};

template<typename... Args>
void print (Args... args) {
    ( std::cout << ... << AddSpace(args) ) << '\n';
}
```

```cpp
// create shared pointer to complex<float> initialized by 4.2 and 7.7:
auto sp = std::make_shared<std::complex<float>>(4.2, 7.7);
```

```cpp
std::thread t (foo, 42, "hello");  // call foo(42,"hello") in a separate thread
```

```cpp
std::vector<Customer> v;
...
v.emplace("Tim", "Jovi", 1962);  // insert a Customer initialized by three arguments
```

```cpp
namespace std {
    template<typename T, typename... Args> shared_ptr<T>
    make_shared(Args&&... args);

    class thread {
    public:
        template<typename F, typename... Args>
        explicit thread(F&& f, Args&&... args);
        ...
    };

    template<typename T, typename Allocator = allocator<T>>
    class vector {
    public:
        template<typename... Args> reference emplace_back(Args&&... args);
        ...
    };
}
```

```cpp
// args are copies with decayed types:
template<typename... Args> void foo (Args... args);
// args are nondecayed references to passed objects:
template<typename... Args> void bar (Args const&... args);
```

```cpp
template<typename... T>
void printDoubled (T const&... args)
{
    print (args + args...);
}
```

```cpp
std::string("hello") + std::string("hello"),
std::complex<float>(4,2) + std::complex<float>(4,2);
```

```cpp
template<typename... T>
void addOne (T const&... args)
{
    print (args + 1...);    // ERROR: 1... is a literal with too many decimal points
    print (args + 1 ...);  // OK
    print ((args + 1)...); // OK
}
```

```cpp
template<typename T1, typename... TN>
constexpr bool isHomogeneous (T1, TN...)
{
    return (std::is_same<T1,TN>::value && ...);  // since C++17
}
```

```cpp
isHomogeneous(43, -1, "hello")
```

```cpp
std::is_same<int,int>::value && std::is_same<int,char const*>::value
```

```cpp
isHomogeneous("hello", " ", "world", "!")
```

```cpp
template<typename C, typename... Idx>
void printElems (C const& coll, Idx... idx)
{
    print (coll[idx]...);
}
```

```cpp
std::vector<std::string> coll = {"good", "times", "say", "bye"};
printElems(coll,2,0,3);
```

```cpp
print (coll[2], coll[0], coll[3]);
```

```cpp
template<std::size_t... Idx, typename C>
void printIdx (C const& coll)
{
    print(coll[Idx]...);
}
```

```cpp
std::vector<std::string> coll = {"good", "times", "say", "bye"};
printIdx<2,0,3>(coll);
```

```cpp
template<typename... Elements>
class Tuple;

Tuple<int, std::string, char> t;    // t can hold integer, string, and character
```

```cpp
template<typename... Types>
class Variant;

Variant<int, std::string, char> v;  // v can hold integer, string, or character
```

