# Operator Functions and Implicit Conversions

As noted earlier in this and previous chapters, allowing implicit conversions from double to Box is not a good idea. Because such conversions would lead to unpleasant results, the corresponding single-argument constructor for Box should really be explicit. But this is not the case for all single-argument constructors. The Integer class you worked on earlier during the exercises of Chapter 12, for instance, provides a good example. At its essence, this class looked like this:

```
```cpp
class Integer
{
public:
    Integer(int value = 0) : m_value{value} {}
    int getValue() const { return m_value; }
    void setValue(int value) { m_value = value; }
private:
    int m_value;
};
```
```

For this class, there is no harm in allowing implicit conversions. The main reason is that Integer objects are much closer to ints than Boxes are to doubles. Other examples of harmless (and convenient!) implicit conversions you already know about are those from string literals to std::string objects or T values to std::optional<T> objects.

For classes that allow implicit conversions, the general guideline for overloading operators as member functions typically changes. Consider the Integer class. Naturally, you’d like binary arithmetic operators such as operator+() for Integer objects. And, of course, you’d like them to work also for additions of the form Integer + int and int + Integer. Obviously, you could still define three operator functions like we did for the operator+() of Integer and Box—two member functions and one nonmember one. But there is an easier option. All you need to do is define one single nonmember operator function as follows:

```
```cpp
Integer operator+(const Integer one, const Integer& other)
{
    return one.getValue() + other.getValue();
}
```
```

Put this function together with our simple class definition of Integer in a integer module. Add similar functions for -, *, /, and %. Because int values implicitly convert to Integer objects, these five operator functions then suffice to make the following test program work. Without relying on implicit conversions, you would’ve needed no less than 15 function definitions to cover all possibilities!

```
```cpp
// Ex13_07.cpp
// Implicit conversions reduce the number of operator functions
import <iostream>;
import integer;

int main()
{
    const Integer i{1};
    const Integer j{2};
    const auto result = (i * 2 + 4 / j - 1) % j;
    std::cout << result.getValue() << std::endl;
}
```
```