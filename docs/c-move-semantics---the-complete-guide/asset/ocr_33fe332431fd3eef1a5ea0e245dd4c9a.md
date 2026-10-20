The fact is that with corresponding getters, the class no longer guarantees that the value as int and string match, which is probably a class invariant here (implicitly or explicitly stated). You might think that the worst consequence is that the value (which is unspecified now) looks different depending on how you use it, but there is no problem using it because it is still a valid int or string.

However, code counting on this invariant might be broken. That code might assume that the string representation has at least one digit. For example, if it searches for the first or last digit, you will definitely find one. For a moved-from string, which is typically empty, this is no longer the case. Therefore, code not double-checking whether there is any character in the string value, might run into unexpected undefined behavior.

Again, it is up to the designer of the class how to deal with this problem. However, if you follow the rule of the C++ standard library, you should leave your moved-from object in a valid state, which might mean that you introduce a possible state that represents “I do not have any value.”

In general, when the state of an object has members that depend on each other in some way, you have to explicitly ensure that the moved-from state is in a valid state. Examples where this might be broken are:

+   - We have different representations of the same value but some of them were moved away.
+   - A member such as a counter corresponds with the number of elements in a member.
+   - A Boolean value claims that a string value was validated but the validated value was moved away.
+   - A cached value for the average values of all elements is still there but the values (being in a container member) were moved away.

Note again that this class worked fine before C++11, where move semantics was not supported. The invariant is broken when switching to C++11 or later and moved-from objects are used.

# 6.3.3 Breaking Invariants Due to Moved Pointer-Like Members

The third reason for move operations breaking invariants relates to objects with members that have pointer-like semantics such as a (smart) pointer.

Consider the following example of a class where objects use a std::shared_ptr<> to share an integral value:

```
class SharedInt {
    private:
        std::shared_ptr<int> sp;
    public:
        explicit SharedInt(int val)
            : sp{std::make_shared<int>(val)} {
        }

        std::string asString() const {
            return std::to_string(*sp);    // OOPS: assume there is always an int value
        }
};
```