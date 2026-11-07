```
```cpp
std::string toString() const {
    return std::format("hr={}, min={}, sec={}", m_hr, m_min, m_sec);
}

// <=> operator automatically supports equality/relational operators
auto operator<=>(const Time& t) const noexcept = default;
private:
    int m_hr{0};
    int m_min{0};
    int m_sec{0};
};

int main() {
    const Time t1(12, 15, 30);
    const Time t2(12, 15, 30);
    const Time t3(6, 30, 0);

    std::cout << std::format("t1: {}\nt2: {}\nt3: {}\n\n",
                t1.toString(), t2.toString(), t3.toString());
```

```

```
```text
t1: hr=12, min=15, sec=30
t2: hr=12, min=15, sec=30
t3: hr=6, min=30, sec=0
```
```

Fig. 11.6 | C++20 three-way comparison (spaceship) operator. (Part 2 of 2.)

In main, lines 26–28 create three Time objects that we’ll use in various comparisons, then display their string representations. Time objects t1 and t2 both represent 12:15:30 PM, and t3 represents 6:30:00 AM. The rest of this program is broken into smaller pieces for discussion purposes.

# With <=>, the Compiler Supports All the Comparison Operators

When you let the compiler generate the overloaded three-way comparison operator (<=>) for you, your class supports all the relational and equality operators, which we demonstrate in lines 34–46. In each case, the compiler rewrites an expression like

```
```cpp
t1 == t2
```
```

into an expression that uses the <=> operator, as in

```
```cpp
(t1 <=> t2) == 0
```
```

The expression t1 <=> t2 evaluates to 0 if the objects are equal, a negative value if t1 is less than t2 and a positive value if t1 is greater than t2. As you can see, lines 34–46 compiled and produced correct outputs, even though class Time did not define any equality or relational operators.