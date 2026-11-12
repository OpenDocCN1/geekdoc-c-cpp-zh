If a *mem-initializer-id* is ambiguous because it designates both a direct non-virtual base class and an inherited virtual base class, the *mem-initializer* is ill-formed.

Here, C::C(): A() is ill-formed : which A ?

# *** Question 199    pack expansion and initializer

Is this program valid one ?

```
~~~cpp
1 template<class... Mixins>
2 class X : public Mixins...
3 {
4 public:
5     X(const Mixins&... mixins)
6         :
7         Mixins(mixins)... { }
8 };
~~~
```

# Solution of Question 199

Yes. A *mem-initializer* followed by an ellipsis is a *pack expansion* that initializes the base classes specified by a pack expansion in the *base-specifier-list* for the class.

# *** Question 200    non-trivial constructor

Is this program valid one ?

```
~~~cpp
1 struct W { int j; };
2 struct X : public virtual W { };
3 struct Y
4 {
5     int *p;
6     X x;
7     Y() : p(&x.j) { }
8 };
~~~
```

# Solution of Question 200

No.

For an object with a non-trivial constructor, referring to any non-static member or base class of the object before the constructor begins execution results in undefined behavior.

For an object with a non-trivial destructor, referring to any non-static member or base class of the object after the destructor finishes execution results in undefined behavior.

Here, `Y() : p(&x.j)` will lead to undefined behavior because *x* is not yet constructed.

# **** Question 201    initializer and this

Review the program.