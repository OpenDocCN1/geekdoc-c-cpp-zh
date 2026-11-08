
```cpp
using plant::operator<<;           // without it 'cout << oak' won't work
std::cout << oak << "\n";
}
```

**Listing 13.1** You define a namespace with “namespace”.

I have packed all sorts of things into the `plant` namespace for demonstration purposes:

- The `plant::Tree` custom data type
- A `operator<<` free function
- Two type aliases, `ConiferousTree` and `BroadleafTree`
- Another namespace

The two type aliases are meant to suggest that you might plan to separate the classes `ConiferousTree` and `BroadleafTree` from `Tree` in the future and write custom classes for them, but for now they are still identical.

You can, if it seems sensible to you, nest namespaces almost arbitrarily and group your project this way. I have packed another element into the `exampleNames` embedded namespace: variables such as `oakName` and the like.

You can also place constants and templates in a namespace. Only macros are not affected by namespaces; see Chapter 21.

`main` must be outside of any namespace; otherwise, the compiler will not find the function as an entry point. In this main, I refer to `plant::ConiferousTree` and `plant::BroadleafTree` with the namespace qualifier. Alternatively, the following would have worked:

```cpp
using plant::ConiferousTree; using plant::BroadleafTree;
ConiferousTree pine{ pineName };
BroadleafTree oak{ oakName };
```

Or simply:

```cpp
using namespace plant;
ConiferousTree pine{ pineName };
BroadleafTree oak{ oakName };
```

I also chose this approach for `using namespace plant::exampleNames`. As a reminder: you should only include an entire namespace with `using namespace` locally—for example, within a function—but never globally in a `*.cpp` file—and certainly not in a header file.

Because `fir` is a local variable in `main`, you can call `print` as a method:

```cpp
fir.print(std::cout); std::cout << "\n";
```

It’s a bit trickier with `operator<<`. If you simply write `std::cout << oak`, it will cause an error because the compiler looks for a suitable free function in all available namespaces (for operators, `std` is also searched). So it looks for the following:

- `operator<<(std::ostream&, const Tree&)` — globally, the level where `main` is
- `std::operator<<(std::ostream&, const Tree&)` — where `std` is searched
- `plant::exampleNames::operator<<(std::ostream&, const Tree&)` — because `using namespace plant::exampleNames` was previously declared

The overload for `Tree` is in namespace `plant`:

```cpp
plant::operator<<(std::ostream&, const Tree&);
```

To use an operator defined within a namespace, you must first make it available so that it is included in the search. There are two options here:

- using `plant::operator<<` — to only fetch the operator
- using namespace `plant` — to fetch everything from the namespace

Namespaces are also useful for separating things that might otherwise conflict. Operators are good candidates here. You might have two `operator<<` variants, as in the following listing.

```cpp
namespace plant {
    // ... as before ...
    std::ostream& operator<<(std::ostream&, const Tree&) {...};
    namespace debug {
        std::ostream& operator<<(std::ostream&, const Tree&) {...};
    }
}
plant::Tree tree{"MyTree"};
void run() {
    using namespace plant;
    cout << tree << "\n";
}
void diagnostic() {
    using namespace plant::debug;
    cout << tree << "\n";
}
int main() {
    run();
    diagnostic();
}
```

**Listing 13.2** In separate namespaces, you can define the same operators.

Depending on the need, you include the desired `operator<<` using a using directive. Unlike functions or types, you cannot specify the scope with operators; `plant::Tree tree{"x"}` works, but `cout << plant::Tree;` does not work. Instead, you could write `plant::operator<<(cout, tree)`, but that makes operators pointless, as you might as well define a function or method.

So if you are tempted to always define operators in the global namespace, you don't need to do that if you know that using `plant::operator<<` also helps.

## Use Namespaces

If you want to structure your project cleanly, use namespaces. I recommend using one main namespace per custom library. Whether you want to subdivide this namespace further depends on the requirements.

By the way, you can extend a namespace later without any problem and split it into two or more files. Simply put everything you want in each file into namespace plant { ... }, and the namespace will fill up from file to file.

### 13.2 Anonymous Namespace

You can also define a namespace without its own identifier. This then has a special meaning. For the purposes of the next listing, assume that you have several files here.

```cpp
// https://godbolt.org/z/e3d55zvT8
// module.hpp
#include <string>
#include <iostream>
namespace plant {
    class Tree {
        std::string name_;
    public:
        explicit Tree(const std::string_view name);
        void print(std::ostream& os) const;
    };
    std::ostream& operator<<(std::ostream& os, const Tree& arg);
}

// module.cpp
#include "module.hpp"
namespace { // anonymous namespace
    std::string PREFIX = "TREE:";
    void printInfo(std::ostream& os) {
        os << "Author: Torsten T. Will\n";
    }
}
bool debug = false;  // global, no namespace
namespace plant {
    Tree::Tree(const std::string_view name)
        : name_(name) {}
    void Tree::print(std::ostream& os) const {
        os << PREFIX << name_;
    }
    std::ostream& operator<<(std::ostream& os, const Tree& arg) {
        if(debug) printInfo(os);
        arg.print(os); return os;
    }
}

// main.cpp
#include "module.hpp"
int main() {
    plant::Tree x{"x"};
    x.print(std::cout); std::cout << "\n";
}
```

**Listing 13.3** An anonymous namespace makes definitions local to the current file.

You see three files here:

- `module.hpp`—interface to class Tree with the method declarations
- `module.cpp`—implementation of the Tree class, with some helpers in an anonymous namespace and a global debug variable
- `main.cpp`—uses the interface

So, you have two modules and a header. If you were to list all the identifiers defined in all modules, you would find that there are no overlaps. There must not be any. All defined identifiers of all modules must be distinct from each other.

For example, you could not define a `int debug = 55;` global variable in `main.cpp`. The compiler would detect during linking that the identifier debug exists multiple times and would produce an error. This is because in `module.cpp`, a debug is already defined; it is not in any namespace.

The set of identifiers can become very confusing in large projects, especially when you also use third-party libraries. You get a large number of identifiers delivered with them, which your identifiers must also not overlap with.

The first precaution for this is to use namespaces. The identifier of the namespace is part of the entire identifier name. This way, `plant::Tree` and `algo::Tree` would not interfere with each other.

The second measure is to use an *anonymous namespace* for what is not needed in other modules. `main.cpp` is not concerned with `PREFIX`. And the `printInfo` function is only used within `module.cpp`. By encapsulating these two identifiers within a namespace `{...}`, they are only visible within the current module. They no longer interfere with another module.

### 13.3 “static” Makes Local

For exactly this purpose, you can also use the keyword `static`. Instead of opening an anonymous namespace, you write `static` before the variables and functions. You achieve the same thing: the name of the variable or function is only visible within this module. Other modules can use the same name without the compiler complaining.

It would look like this for `module.cpp`:

```cpp
// https://godbolt.org/z/fZyZjgrW
// module.cpp
#include "module.hpp"
static std::string PREFIX = "TREE:";
static void printInfo(std::ostream& os) {
    os << "Author: Torsten T. Will\n";
}
bool debug = false;
// rest as before
```

The debug variable is not yet static. As a result, no other module can define a global function or global variable debug, but that is intentional here. Because although debug is not in the `module.hpp` header, someone with enough insider knowledge (the author) can manipulate the variable. Consider this an excursus as it should not be part of usual programming practice to hide and change variables in this way. In some other module of the project, someone can manipulate the variable with

```cpp
extern bool debug;
```

and declare and then manipulate it with `debug = true;`. This can be both good and bad. For a debugging switch, it might just be permissible. Otherwise, put identifiers that should not be exported into an anonymous namespace (or declare them `static`).

An anonymous namespace has the great advantage over `static` that it also protects its own types from spilling over into other modules. You cannot protect `struct`, `class`, or using X = Y from export with a `static`. Within a namespace `{...}`, however, these things are safe.
