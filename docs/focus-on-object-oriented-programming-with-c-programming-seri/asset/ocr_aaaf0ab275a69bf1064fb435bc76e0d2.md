# This Pointer

At this point you might be wondering how member functions are implemented in C++. Consider the following class:

```
class Alpha {
    private:
        int a, b, c;
    public:
        void foo(int x, int y, int z);
};

int main() {
    Alpha a1, a2;
    :
    :
}
```

An ordinary member function is invoked as:

```
a1.foo(i, j, k);
a2.foo(i, j, k);
```

The code for the member function is kept within the class Alpha. When foo() is invoked by object a1, the member function foo() operates on the private data of object a1. Likewise, when foo() is invoked by object a2, the member function foo() operates on the private data of object a2. How does the member function know what object it's dealing with, and which private data to manipulate?

Let's explore the invocation of the member function foo():

```
a1.foo(i, j, k);
```

How many arguments are passed to the function? The answer may surprise you. It is 7!

+   * The explicit argument list contains 3 arguments: i, j, k.