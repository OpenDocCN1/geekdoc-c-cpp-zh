Similarly, a statement such as:

```
class_name *p = new class_name;
```

invokes the default constructor, that we'll see next.

Test *p = new Test;

If a constructor accepts a single argument, it is allowed to initialize an object with a value of the same type as the argument. For example, if the following constructor is defined in class A:

```
A(int v); it is allowed to write: A a = 20;
```

Such initialization invokes the constructor. Notice that this feature can cause problems, but it can be disabled, as we'll discuss in Chapter 19.

# Calling the Destructor

As we said, the destructor is called automatically when the object goes out of scope or destroyed with the delete operator. Consider the following class:

```
class T
{
public:
  T() {};n  ~T() {}
};
```

The question is, can we explicitly call the destructor, that is, can we write something similar to:

```
T t;
~T();
```

The answer is yes; we can call it directly, but do not do it, as unexpected errors may occur. You do not need to call the destructor, it will be called automatically. However, I just mention it without further analysis, there may be some special cases where the destructor should be explicitly called.

Another possible question might be, can the destructor be private? Yes, but check the following program:

```
#include <iostream> // Example 17.6
class T
{
private:
  ~T(std::cout << "Out\n");
public:
  void end{this;} // The object is destroyed.
  T() {}
};
```