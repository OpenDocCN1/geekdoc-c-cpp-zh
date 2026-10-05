# 25 • Namespaces, Type Cast Operators, and Smart Pointers 811

Sum up, the using declaration makes only one name available, while the using directive makes all names available. As I mentioned in Chapter 1, if I don't have to add the namespace many times, I prefer to use the :: operator. If it is many or only a few names are used from the namespace, I prefer to use using declarations, so that readers code can see what elements of the namespace are needed. If many names are used, for more convenience and simplicity in the code, I may use the using directive. However, if I am going to use many namespaces, I don't use it, since if many names are made available, the possibility of name conflicts increases. And if there is no conflict now, it may happen in the future with a new version of the code that may add a common name.

# Combine using Declarations and using Directives

In a namespace we are allowed to use both using declarations and directives. For example:

```
namespace C
{
    using std::cout;
    using namespace A;

    void test() {cout << var;}
    
}
```

Now, if we want to access the var variable of A (e.g., in test()) we can write directly since A is contained in C. For the same reason, the statement:

```
using namespace C;
```

makes available all the elements of A and C.
Let's look at another example where their combination prevents conflicts.

```
namespace Name_1
{
    class A {...};
    class B {...};
}
```

```
namespace Name_2
{
    class A {...};
    class B {...};
}
```

```
namespace Name_3
{
    using namespace Name_1; // Makes available all the names of Name_1.
    using namespace Name_2; // Makes available all the names of Name_2.
    using Name_1::A;
    using Name_2::B;
```

![](bbox=[0.083, 0.966, 0.105, 0.982])