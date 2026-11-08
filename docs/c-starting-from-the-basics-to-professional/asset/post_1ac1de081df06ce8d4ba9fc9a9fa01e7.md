
## CHAPTER 13: OPERATOR OVERLOADING

- As a rule, you cannot override built-in operators. The signature of an overloaded operator thus typically involves at least one class type. We will discuss the term *overriding* in more detail in the next chapter, but in this case it means you cannot modify the way existing operators operate on fundamental types or array types. In other words, you cannot, for instance, make integer addition perform multiplication. While it would be great fun to see what would happen, we're sure you'll agree that this is a fair restriction.

These restrictions notwithstanding, you have quite some freedom when it comes to operator overloading. But it's not because you can overload an operator that it necessarily follows that you should. When in doubt, always remember the following key guideline:

> **Tip** The main purpose of operator overloading is to increase both the ease of writing and the readability of code that uses your class. The fact that overloaded operators make for more compact code should always come second. Compact yet incomprehensible or even misleading code is no good to anyone. Making sure your code is both easy to write and easy to read is what matters. One consequence is that you should, at all costs, avoid overloaded operators that do not behave as expected from their built-in counterparts.

Obviously, it’s a good idea to make your version of a standard operator reasonably consistent with its normal usage, or at least intuitive in its meaning and operation. It wouldn’t be sensible to produce an overloaded + operator for a class that performed the equivalent of a multiplication. But it can be more subtle than that. Suppose we defined the equality operator for Box objects like this:

```cpp
bool Box::operator==(const Box& aBox) const { return volume() == aBox.volume(); }
```

Seems sensible, and it’s nicely analogous to the < operator we defined before. Still, this unconventional definition of operator == could easily lead to confusion. Suppose, for example, that we create these two Box objects:

```cpp
Box oneBox { 1, 2, 3 };
Box otherBox { 1, 1, 6 };
```

Would you then consider these two boxes “equal”? Most likely the answer is that you don’t. After all, they have significantly different dimensions. If you order a box with dimensions 1 x 2 x 3, you wouldn’t be pleased if you receive one with dimensions 1 x 1 x 6. Nevertheless, with our definition of operator ==(), the expression oneBox == otherBox would evaluate to true. This could easily lead to misunderstandings and therefore bugs.

This is how most programmers would expect an equality operator for Box to be defined:

```cpp
bool Box::operator==(const Box& otherBox) const
{
    return m_width == otherBox.m_width
        && m_length == otherBox.m_length
        && m_height == otherBox.m_height;
}
```

Which definition you use will depend on your application and how you expect Boxes to be used. But in this case we believe it is best to stick with our second, more intuitive, definition of operator==. (The reason is that it probably leads to the least number of surprises. When programmers see ==, they think “is equal to,” not “has same values as.” If need be, you can always introduce a member function called hasSameValues() to check for equal values. Yes, hasSameValues() involves more typing than ==, but it does ensure your code remains readable and predictable—and that is far more important!

Most of the remainder of this chapter is about teaching you similar corresponding operator overloading. You should deviate from these conventions only if you have a good reason.

> **Caution** One concrete consequence of our key guideline for operators is that you should never overload the logical operators && or ||. If you want logical operators for objects of your class, overloading & and | instead is generally preferable.

The reason is that overloaded && and || will never behave quite like their built-in counterparts. Recall from Chapter 4 that if the left operand of the built-in && operator evaluates to false, its right operand does not get evaluated. Similarly, for the built-in || operator, the right-side operand is never evaluated if the left-side operand evaluates to true. You can never obtain this so-called short-circuit evaluation with overloaded operators.[^1] Because an overloaded operator is essentially equivalent to a regular function call, all operands to an overloaded operator are always evaluated before entering the function’s body. For overloaded && and || operators, this means that both the left and right operands will always be evaluated. Because users of any && and || operator will expect the familiar short-circuit evaluation, overloading them would thus easily lead to some subtle bugs. When overloading & and | instead, you make it clear not to expect short-circuit evaluation.

### Operator Function Idioms

The remainder of this chapter is all about introducing commonly accepted patterns and best practices regarding the when and how of operator overloading. There are only a few real restrictions for operator functions. But with great flexibility comes great responsibility. We will teach you when and how to overload various operators and the various conventions C++ programmers typically follow in this context. If you adhere to these conventions, your classes and their operators will behave predictably, which will make them easy to use and thus reduce the risk of bugs.

All the binary operators that can be overloaded always have operator functions of the form that you’ve seen in the previous section. When an operator, Op, is overloaded and the left operand is an object of the class for which Op is being overloaded, the member function defining the overload is of the following form:

```cpp
ReturnType operator Op(Type right_operand);
```

If you overload the spaceship operator, <=>, for your class, C++20 automatically gives you complete support for all four relational operators (<, >, <=, and >=), free of charge. And if you overload ==, C++20 similarly makes sure != works as well. There’s thus rarely a need to define custom <, >, <=, >=, or != operators anymore in C++20. The only comparison operators you still have to overload are <=> and ==. Here is how you do this for the Box class:

```cpp
// Box.cpp
export module box;

import <compare>;  // For std::partial_ordering (see Chapter 4)

export class Box
{
public:
    // ...
    // Same constructors and member functions as in Ex13_02, except no operator<.

    std::partial_ordering operator<=>(const Box& otherBox) const
    {
        return volume() <=> otherBox.volume();
    }
    std::partial_ordering operator<=>(double otherVolume) const
    {
        return volume() <=> otherVolume;
    }

    bool operator==(const Box& otherBox) const
    {
        return m_length == otherBox.m_length
            && m_width == otherBox.m_width
            && m_height == otherBox.m_height;
    }

private:
    double m_length {1.0};
    double m_width {1.0};
    double m_height {1.0};
};
```

An overload of the <=> operator should return one of the three comparison category types defined by the <compare> module: std::partial_ordering, weak_ordering, or strong_ordering (see Chapter 4). Here we opted for std::partial_ordering.

As argued before, we do not consider two boxes with the same volume to be equal, unless they also have the same dimensions. Labeling them equivalent makes sense, yes, but they are not equal (see also Chapter 4 for the difference between “equivalent” and “equal”). So that rules out std::strong_ordering.

Which leaves partial_ordering and weak_ordering. In Chapter 4 you saw that comparing two floating-point values with operator <=> results in a value of type partial_ordering. The reason being that one or both operands could be not-a-number. While we do not expect Boxes to ever have dimensions that are not-a-number, there is nothing in place to prevent this either (exceptions could help with this; see Chapter 16). Which means that, at least in theory, the volume() of a Box could be not-a-number as well.
