# 23 · Class Templates 757

```
public:
    template <typename T2> class B {
    private:
        T2 p;
    public:
        B(p = 5);
        void show(const std::cout& p << << '\n');
    };
    A(int i) { m = i; }
    B<int> b;
    void show() const {std::cout << m << ' '}
    template <typename T3> void f(T3 j) const {std::cout << j << '\n'};
};

int main() {
    A<double> a(1.2);
    a.show();
    a.b.show();
    a.f("text");
    return 0;
}
```

The class template contains the template of the B class. When an a is created, T becomes double, and the constructor makes the value of m equal to 1.2. The b object of the B<int> class is created. T becomes int, the default constructor B() is called and b.p becomes 5. I added the f() function template. When called, the compiler checks the type of the argument passed to T3 and creates the definition of f(). Thus, the program displays 1.2 5 text. If we want to define the function template outside the class template, we first write the parameter list of the class and then that of the function.
For example:

```
template <typename T1>
    template <typename T3> void A<T1>::f(T3 j)
```

Note that a template member function is not allowed to be virtual. For example, it is wrong to write:

```
class A {
    ...
    template <typename T> virtual void f(const T& t); // Wrong.
};
```

The reason this is not allowed is that the implementation with the array of the virtual functions (vtable) mentioned in Chapter 20 would become more complicated, every time f() is called with a new type of argument a new entry for the A class would have to be added in the array of its virtual functions.