# Friends

One of object-oriented programming's main gifts is the encapsulation of data in classes. We've seen many examples of this data-hiding concept and we've considered its benefits of reduced maintenance and easier debugging.

Like many rules in life and programming, those of data-hiding may be broken. In C++, you can break encapsulation's rules by using friends, although you do so at some risk to your program's welfare. The friend mechanism gives non-members of the class access to the private members of the class.

C++ classes can declare two kinds of friends:

+   - An entire class may be a friend of another class.
+   - A single function may be declared as a friend.

Note: If friends have a counterpart in other languages, it's the `goto` statement. Like `goto`, a friend enables you to break the rules intended to help you write reliable code. Don't interpret the following as an endorsement of friends. Top C++ programmers avoid using friends unless absolutely necessary. Needless to say, the use of friend functions in C++ is controversial.

# Friend Classes

A class may declare another class as a friend. The first class (the one that declares the friend) gives another class (the friend) permission to access all private members of the first class. Note that public members are always accessible, so you don't need to declare a class a friend to give it access to public members.

Typically, friend classes are used when two unrelated classes require access to the class's private parts. For example:

```
class Alpha {
private:
    double value;
public:
    Alpha() { value = 3.14159; }
};
```