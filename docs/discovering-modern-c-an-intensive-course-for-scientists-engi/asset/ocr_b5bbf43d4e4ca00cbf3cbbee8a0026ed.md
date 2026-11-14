When constructors with the same signature exist in both classes, that from the derived class is preferred.

So far, we have applied three of the four before-mentioned basic principles: encapsulation, inheritance, and sub-typing. But there is still something missing and we will introduce it now.

# ## 6.1.3 Virtual Functions and Polymorphic Classes

The full potential of object-oriented programming is only unleashed with virtual functions. Their presence changes the behavior of a class fundamentally, leading to the following:

> **Definition 6-1 (Polymorphic Types).** Classes containing one or more **virtual** functions are called **_Polymorphic Types_**.

We continue with the preceding implementation and only add the attribute virtual to the method `all_info()`:

```
```cpp
class person
{
    virtual void all_info() const { cout << "My name is " << name << endl; }
    ...
};
```
```

```
```cpp
class student
    : public person
{
    virtual void all_info() const {
        person::all_info(); // call all_info() from person
        cout << "I passed the following grades: " << passed << endl;
    }
    ...
};
```
```

The double colons `::` that we have seen as namespace qualifications (§3.2) can similarly qualify a class from which we call a method. This requires of course that the method is accessible: we cannot call a private method from another class, not even a base class.

Printing the information with the polymorphic class yields a completely different result all of a sudden:

```
```
[person] My name is Mark Markson
[student] My name is Tom Tomson
I passed the following grades: Algebra, Analysis
[person] My name is Tom Tomson .
[student] My name is Tom Tomson
I passed the following grades: Algebra, Analysis
[student] My name is Tom Tomson
I passed the following grades: Algebra, Analysis
```
```