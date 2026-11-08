```
```cpp
public:
    static inline size_t count = 0;    // counts created instances
    explicit Keyboard() : nr_{count++} {
        std::cout << " Keyboard() nr:" << nr_ << "\n";
    }
};
Keyboard& getKeyboard() {
    std::cout << " getKeyboard()\n";
    static Keyboard keyboard{};         // static local variable
    return keyboard;
}
void func() {
    std::cout << " func...\n";
    Keyboard& kbF = getKeyboard();
}
int main() {
    std::cout << " kbA...\n";
    Keyboard& kbA = getKeyboard();
    func();
    std::cout << " kbB...\n";
    Keyboard& kbB = getKeyboard();
    std::cout << "count:" << Keyboard::count << "\n";
}
```
```

**Listing 13.5** A local static variable is initialized once and reused thereafter.

Here you see the implementation of the so-called Meyer’s Singleton pattern. A *singleton* is a way to always get the same instance of a class with each use. The uses can also come from different parts of the program, as seen here from `func()` and `main()`; because both use the `getKeyboard()` free function, they also receive the same Keyboard& reference and thus the same object.

Singletons are particularly popular in programs with multiple threads. For example, imagine that your program has multiple *threads* (simultaneously running program strands), and each wants to read from the keyboard—and for that, it needs a Keyboard class. The Keyboard class establishes the connection to the one keyboard actually connected to the computer. It would be helpful if it were always the same keyboard. This is what the `getKeyboard()` function is supposed to provide in the example.

```
```cpp
Keyboard& getKeyboard() {
    cout << " getKeyboard()\n";
    static Keyboard keyboard{}; // static local variable
    return keyboard;
}
```
```

**Listing 13.6** The Meyers Singleton.