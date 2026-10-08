Interestingly, this definition makes the example above work as specified. Now we just have to figure out why it works. When we say **Larger_than(31)** we (obviously) make an object of class **Larger_than** holding **31** in its data member **v**. For example:

```
```
find_if(v.begin(),v.end(),Larger_than(31))
```
```

Here, we pass that object to **find_if()** as its parameter called **pred**. For each element of **v**, **find_if()** makes a call

```
```
pred(*first)
```
```

This invokes the call operator, called **operator()**, for our function object using the argument ***first***. The result is a comparison of the element’s value, ***first***, with **31**.

What we see here is that a function call can be seen as an operator, the “( ) operator,” just like any other operator. The “( ) operator” is also called the *function call operator* and the *application operator*. So ( ) in **pred(*first*)** is given a meaning by **Larger_than::operator()**, just as subscripting in **v[i]** is given a meaning by **vector::operator[]**.

# 21.4.1 An abstract view of function objects

We have here a mechanism that allows for a “function” to “carry around” data that it needs. Clearly, function objects provide us with a very general, powerful, and convenient mechanism. Consider a more general notion of a function object:

```
```
class F {          // abstract example of a function object
  S s;             // state
public:
  F(const S& ss) :s(ss) { /* establish initial state */ }
  T operator() (const S& ss) const
  {
    // do something with ss to s
    // return a value of type T (T is often void, bool, or S)
  }

  const S& state() const { return s; }   // reveal state
  void reset(const S& ss) { s = ss; }    // reset state
};
```
```

An object of class **F** holds data in its member **s**. If needed, a function object can have many data members. Another way of saying that something holds data is that it “has state.” When we create an **F**, we can initialize that state. Whenever we want to, we can read that state. For **F**, we provided an operation, **state()**, to