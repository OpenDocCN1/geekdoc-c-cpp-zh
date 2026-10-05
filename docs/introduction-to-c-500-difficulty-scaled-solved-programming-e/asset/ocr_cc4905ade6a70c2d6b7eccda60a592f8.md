# 728 Introduction to C++

I just wanted to show you an example that combines exceptions of basic and user-defined types. In large applications, where exceptions from different libraries can be thrown, it is safer to choose your own types than basic types (e.g., integer values) to avoid the case that the same exception is used by some library.

Let me ask you, could we pass an object of a reference and catch(Err_Rpt err); or pass a reference of the basic type and catch(int& code); No problem. in fact, when an exception is thrown, even if a reference is specified, what is really passed is the copy of the object. And so it should be, the Err_Rpt object does not exist after the end of the check_pwd(). In particular, when an exception is thrown, the try block is exited and it is out of scope, if it is copied to a temporary object and then it is destroyed. There is by no problem to throw local objects from inside the try block. Note that in a multi-level exception system, the object can be copied multiple times if it is finally caught, but it is better not to contain too much information. The logical question to make is, since the object is copied, why to use a reference? I'll answer you in the next section.

# Exceptions and Inheritance

The answer to the previous question is, as we know from Chapter 20, a reference to the base class can refer to objects of classes derived from it. For example, in the following program we have three classes of exceptions that are related to each other by inheritance:

```
#include <iostream> // Example 22.4
class Err {
public:
    virtual void show() const {std::cout << "Err1\n";}
};
class Err2 : public Err {
public:
    virtual void show() const override {std::cout << "Err2\n";}
};
class Err3 : public Err2 {
public:
    virtual void show() const override {std::cout << "Err3\n";}
};
void f();
int main() {
    try {
        f();
    } catch(const Err1& err) {
        err.show();
    }
    return 0;
}
```