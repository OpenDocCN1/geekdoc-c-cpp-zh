
## Copy Assignment Operator

The copy assignment operator is automatically generated when all of the following apply:

- No move constructor is user-declared
- No move assignment operator is user-declared

If generated (implicitly or with `=default`), the copy assignment operator approximately has the following behavior:

```
MyClass& operator = (const MyClass& obj) noexcept-specifier {
    Base::operator=(obj);     //- perform assignments for base class members
    value = obj.value;         //- assign new members
    return *this;
}
```

The generated copy assignment operator first calls the best matching assignment operator of the base class(es) for the passed source object (remember that assignment operators in contrast to copy constructors are *not* called on a top-down basis; they call the base class assignment operator(s) in the implementation). Afterwards it assigns all members of its class (again using the best match).

Note that the generated assignment operator does not check for assignments of objects to themselves. If this is critical, you have to implement the operator yourself.

In addition, the generated copy assignment operator is declared as noexcept if all assignment operations (the assignment of the base class members and the assignment of the new members) give this guarantee.

## Move Assignment Operator

The move assignment operator is automatically generated when all of the following apply:

- No copy constructor is user-declared
- No move constructor is user-declared
- No copy assignment operator is user-declared
- No destructor is user-declared

If generated (implicitly or with `=default`), the move assignment operator approximately has the following behavior:

```
MyClass& operator = (MyClass&& obj) noexcept-specifier {
    Base::operator=(std::move(obj));  //- perform move assignments for base class members
    value = std::move(obj.value);      //- move assign new members
    return *this;
}
```

The generated move assignment operator first calls the best matching move assignment operator of the base class(es) for the passed source object, marked with `std::move()` to pass through its move semantics. Afterwards it move assigns all members of its class (again using the best match).

You might wonder why we still use members of the source object obj after the object was marked with std::move():

```
Base::operator=(std::move(obj)); // - perform move assignments for base class members
```

However, in this case we mark the object for the specific context of a base class, which cannot see the members introduced in this class. Therefore, the derived members have a valid but unspecified state but we can still use the values of the new members.

The generated assignment operator also does not check for assignments of objects to themselves. Thus, in its default behavior, the operator will move assign each member to itself, which usually means that members receive a valid but unspecified value. If this is critical, you have to implement the operator yourself.

In addition, the generated move assignment operator is declared as noexcept if all called assignment operations (the assignments for base class members and the assignments for new members) give this guarantee.

## Other Special Member Functions

Other special member functions do not play such an important role for move semantics:

- **Destructors** are nothing special with move semantics except that their declaration disables the automatic generation of move operations.
- The **default constructor** (the “not-so-special” special member function) is still automatically generated if no other constructor is declared. That is, the declaration of a move constructor disables the generation of a default constructor.

However, note that these special member functions play a role when talking about moved-from states. The state of the default constructor is often the “natural” state of a moved-from object and a moved-from object always should be destructible.

## 3.4 The Rule of Five or Three

Whether and which special member functions are automatically generated depends on a combination of several of the rules just described. Many programmers do not know all these rules. Therefore, even before C++11, the usual guideline is to provide either none or all of the special member functions for copying, assignment, and destruction.

- Before C++11, this guideline was called the **Rule of Three**: The guideline was to either declare all three (copy constructor, assignment operator, and destructor) or none of them.
- Since C++11, the rule has become the **Rule of Five**, which is usually formulated as: The guideline is to either declare all five (copy constructor, move constructor, copy assignment operator, move assignment operator, and destructor) or none of them.

Here, declaring means:

- Either to implement ({...})
- Or to declare as defaulted (=default)
- Or to declare as deleted (=delete)

That is, when one of these special member functions is either implemented or defaulted or deleted, you should implement or default or delete all four other special member functions.

However, you should be careful with this rule. I recommend that you take it more as a guideline to *carefully think* about all of these five special member functions when one of them is user-declared.

As we saw, to enable copy semantics only you should `=default` the copying special member functions without declaring the special move member functions (deleting and defaulting the special move member functions would not work, implementing them makes the class unnecessarily complicated). This option is recommended in particular if the generated move semantics creates invalid states, as we discuss in the section about invalid moved-from states.

When applying this rule of five, it also turned out that sometimes, programmers use it to add declarations for the new move operations without understanding what this means. Programmers were just declaring move operations with `=default` because copy operations were implemented and they wanted to follow the rule of five.

Therefore, I usually teach the *Rule of Five or Three*:

- If you declare the copy constructor, move constructor, copy assignment operator, move assignment operator, or destructor, *think very carefully* about how to deal with the other special member functions.
- If you do not understand move semantics, think only about the copy constructor, copy assignment operator, and destructor if you are declaring one of them. If in doubt, disable move semantics by declaring the copying special member functions with `=default`.

## 3.5 Summary

- Move semantics is not passed through.
- For every class, the move constructor and move assignment operator are automatically generated (unless there is no way to do so).
- User-declaring a copy constructor, copy assignment operator, or destructor disables the automatic support of move semantics in a class. This does not impact the support in derived classes.
- User-declaring a move constructor or move assignment operator disables the automatic support of copy semantics in a class. You get move-only types (unless these special move member functions are deleted).
- Never `=delete` a special move member function.
- Do not declare a destructor if there is no specific need. There is no general need in classes derived from a polymorphic base class.

## Chapter 4

## How to Benefit From Move Semantics

Most of the time, programmers benefit from move semantics automatically. However, even as an ordinary application programmer, you can benefit from move semantics even more when programming slightly differently.

This chapter discusses how to benefit from move semantics in ordinary application code, classes, and class hierarchies beyond the automatic generation of special move member functions. The chapter also introduces corresponding new guidelines.

Note that even several years after introducing move semantics these recommendations are not widely known in the community. In fact, one reason for me to write this book was to make them state of the art for modern C++ programming.

## 4.1 Avoid Objects with Names

As we have seen, move semantics allows us to optimize using a value from a source that no longer needs that value. If compilers automatically detect that a value is used from an object that is at the end of its lifetime, they will automatically switch to move semantics. This is the case when:

- We pass a temporary object that will automatically be destroyed after the statement.
- We return a local object by value.

In addition, we can force move semantics by marking an object with `std::move()`.

Because it is easier to just let compilers do the work, a first consequence of move semantics is the following advice: **avoid objects with names.**

Instead of

```
MyType x{42, "hello"};
foo(x);      // x not used afterwards
```

it would be better to program:

```
foo(MyType{42, "hello"});
```

to automatically enable move semantics.
