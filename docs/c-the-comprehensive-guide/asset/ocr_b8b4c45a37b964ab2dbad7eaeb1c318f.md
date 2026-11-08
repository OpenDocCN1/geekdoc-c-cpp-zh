+   - `operator<<(std::ostream&, const Tree&)` — globally, the level where `main` is
+   - `std::operator<<(std::ostream&, const Tree&)` — where `std` is searched
+   - `plant::exampleNames::operator<<(std::ostream&, const Tree&)` — because `using namespace plant::exampleNames` was previously declared

The overload for `Tree` is in namespace `plant`:

```
plant::operator<<(std::ostream&, const Tree&);
```

To use an operator defined within a namespace, you must first make it available so that it is included in the search. There are two options here:

+   - using `plant::operator<<` — to only fetch the operator
+   - using namespace `plant` — to fetch everything from the namespace

Namespaces are also useful for separating things that might otherwise conflict. Operators are good candidates here. You might have two `operator<<` variants, as in the following listing.

```
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
    cout << tree << "\\n";
}
void diagnostic() {
    using namespace plant::debug;
    cout << tree << "\\n";
}
int main() {
    run();
    diagnostic();
}
```
```

**Listing 13.2** In separate namespaces, you can define the same operators.

Depending on the need, you include the desired `operator<<` using a using directive. Unlike functions or types, you cannot specify the scope with operators; `plant::Tree tree{"x"}` works, but `cout << plant::Tree;` does not work. Instead, you could write