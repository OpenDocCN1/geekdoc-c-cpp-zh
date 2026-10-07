# Chapter 18 Visiting the New C++ Standard

You may recall (from Chapter 12) that you can disable copying by placing the copy constructor and assignment operator in the private section of a class. But using delete is a less devious and more easily understood how to accomplish that end.

What is the effect of disabling copy methods while enabling move methods? Recall that rvalue reference, as used by move operations, binds only to rvalue expressions. This implies the following:

```
SomeClass one;
SomeClass two;
SomeClass three (one); // not allowed, an lvalue
SomeClass four (one + two); // allowed, expression is an rvalue
```

Only the six special member functions can be defaulted, but you can delete with any member function. One possible use is to disable certain conversions. Suppose, for example, that the SomeClass class has a method with a type double parameter:

```
class SomeClass {
public:

	void redo(double);


}
```

Then suppose we have the following code:

```
SomeClass sc;
sc.redo(5);
```

The int value 5 will be promoted to 5.0, and the redo() method will execute. Now suppose the SomeClass definition is modified thus:

```
class SomeClass {
public:

	void redo(double);
	void redo(int) = delete;

}
```

In this case, the method call sc.redo(5) matches the redo(int) prototype. The compiler will later find and also detect that redo(int) is deleted, and it will flag the call as a compile-time error. This illustrates an important fact about deleted functions. They do so as far as function look-up is concerned, but to use them is an error.

# Delegating Constructors

If you provide a class with several constructors, you may find yourself writing the same code over and over. That is, some of the constructors may require you to duplicate code