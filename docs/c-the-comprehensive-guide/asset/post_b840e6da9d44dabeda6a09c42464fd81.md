
## 13.4 “static” Likes to Share

The fact that `static` is also used for a completely different purpose takes some getting used to. You can use it to mark a data field or a method of a class to share it among all instances of the class. Or to put differently:

- **static for a data field**
  While there is always one instance of a normal data field per instance, all instances share a common data field marked as `static`. Therefore, there is exactly one instance of this data field per class and not as many as there are instances.
- **static for a method**
  A static method lacks the `this` pointer. Within the method, there is no connection to a specific instance of the class. Therefore, you do not call the method via an instance with `.` or `->`, but rather via the class name with `::`.

Both variants are similar in that you can access both even if you have not created a single instance yet.

Typical applications are as follows:

- A static data field can count the number of active instances of the class.
- A static method can serve as a *factory* for controlled creation of instances (popular design pattern).

In the following listing, both application possibilities are in use.

```cpp
// https://godbolt.org/z/n4e8xdEGj
#include <iostream> // cout
#include <string>
using std::string;
class Tree {
    static size_t countConstructed_;
    static size_t countDestructed_;
    string kind_;
    Tree(string kind) : kind_{kind}        // private constructor
        { ++countConstructed_; }
public:
    Tree(const Tree& o) : kind_{o.kind_}
        { ++countConstructed_; }
    string getKind() const { return kind_; }
    ~Tree() { ++countDestructed_; }
    static Tree create(string kind) { return Tree{kind}; }
    static void stats(std::ostream& os) {
        os << "Constructed:+" << countConstructed_
           << "  Destructed:-" << countDestructed_ << "\n";
    }
};

size_t Tree::countConstructed_ = 0;
size_t Tree::countDestructed_ = 0;

int main() {
    Tree birch = Tree::create("Birch");
    for(auto kind : {"Ash", "Yew", "Oak"}) {
        Tree temp = Tree::create(kind);
        std::cout << temp.getKind() << "\n";
    }
    Tree::stats(std::cout);
}
```

Listing 13.4 All instances share their “static” data fields and methods.

First, I declared two counters countConstructed_ and countDestructed_. Unlike normal data fields, you unfortunately cannot initialize static data fields within the class. Therefore, you see a repetition of the static data fields with the initialization values outside the class—here, 0 for each.

Note that if the class is defined in a header that may be included by multiple *.cpp files, you must place the initialization definitions in a *.cpp file. Otherwise, the initialization would be performed multiple times in the entire program, or the linker would complain about duplicate definitions.

The static create method is in the public section of the class. This should now be used to create new Tree instances. To prevent anyone from calling it from outside, the constructor has been moved to the private section of the class.

Within the constructor, I increment the countConstructed_ counter. To increment the countDestructed_ counter, I also need the destructor. This should almost always be in the public section of the class.

Tree still needs the copy constructor because create returns the newly created tree as a copy. Copying also creates a new object that should be counted with countConstructed_, so the = default copy constructor is not suitable. As the class currently stands, you could also do without the copy constructor and instead define the move constructor, but that’s just a detail.

You see in main that you can call Tree::create() without a Tree instance already being created. When you are inside the create method, there is no instance whose data fields you can access. You can only access other static data fields and static methods—and constructors.

There is a distinction between calling a static Tree::create() method and a normal tree.getKind() method: the use of the class name instead of the instance variable, as well as the scope operator :: instead of the access point . or the arrow ->, if it is a pointer to an instance.

Similarly, I call `Tree::stats()` at the end. Again, only static data fields are accessed. And the output

```text
Constructed:+4 Destructed:-3
```

proves that each instance accessed the same counter variables in its constructor or destructor. The count is correct because all Tree temp objects in the loop were also destroyed again. Only the local birch variable still exists at the time of the `stats()` call.

## Copy Constructor and Move Constructor

How to make a class that copies itself is detailed in Chapter 16. At this point, you should know that classes can be copied. Sometimes the compiler can set the rules for this, and sometimes you want or need to do it yourself. To do this, declare this constructor:

```cpp
Keyboard(const Keyboard&);
```

In the definition, you then specify how the copying should be done. If you explicitly want to prevent a copy from being possible, write the declaration like this:

```cpp
Keyboard(const Keyboard&) = delete;
```

The same applies to moving. The declaration that you use to declare and simultaneously prevent the move is this:

```cpp
Keyboard(Keyboard&&) = delete;
```

However, this is implicit if you have specified the copy constructor. For more on this, see Chapter 16.

## 13.5 Remote Initialization or “static inline” Data Fields

Assume you have defined a `Tree` class in the `tree.hpp` header and used the header multiple times in your program. Then you must ensure that the initialization of the static data fields is done in exactly one *.cpp file and not in the *.hpp file as they would otherwise be defined multiple times.

Therefore, starting from C++17, in addition to `static`, write the `inline` keyword and set the field directly—that is, the declaration and definition together. The compiler ensures unique initialization:

```cpp
class Tree {
    static inline size_t countConstructed_ = 0;
    static inline size_t countDestructed_ = 0;
    // ...
```

## 13.6 Guaranteed to Be Initialized at Compile Time with “constinit”

Starting from C++20, you can mark global or static variables with `constinit`. This ensures that the compiler guarantees that the variable can be initialized at compile time. The chances are then high that no initialization work needs to be done at run-time.

Even though the sequence of letters `const` appears in this keyword, the variable is not constant. One could say that “constinit is `constexpr` minus `const`”:

```cpp
// https://godbolt.org/z/b9arcEMM1
constinit auto SZ = 10*100-1;                 // global variable
size_t autoincrement() {
    static constinit size_t i = 0;             // local static variable
    return i++;
}
class BraitenbergVehicle {
    inline static constinit size_t count_ = 0;  // class variable
public:
    size_t id;
    BraitenbergVehicle() : id{++count_} {}
    ~BraitenbergVehicle() { --count_; }
};
```

The `SZ`, `i`, and `count_` variables are initialized at compile time. The `i` and `count_` variables are also modified during the program’s execution.

In practice, `constinit` solves the problem in which sometimes the order of initialization of static variables is not clear, and you might not realize that you are accessing a variable that has not been initialized yet. With `constinit`, it is guaranteed that the expression can be evaluated at compile time and is not affected by such problems.

You can use `constinit` together with `extern` and `thread_local`.

## 13.7 “static” Makes Permanent

Similar, but not the same, is the use of `static` with local variables—that is, within a function. When you add `static` to the declaration of a local variable, this variable persists when the program flow leaves the scope and is reused when it is entered again.

```cpp
// https://godbolt.org/z/h5qond6b
#include <iostream>                    // cout
class Keyboard {
    Keyboard(const Keyboard&) = delete; // no copy
    const size_t nr_;                   // current number
```
