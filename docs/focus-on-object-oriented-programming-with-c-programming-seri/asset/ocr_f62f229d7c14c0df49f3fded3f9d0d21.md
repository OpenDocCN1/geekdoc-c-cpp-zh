+   • Another reason for not modifying the Counter class is that we might not have access to its source code, especially if it has been distributed as part of a class library.

To avoid these problems, we can use inheritance to create a new class based on Counter, without modifying Counter itself. We can derive a new class, CountDn, which adds a decrement operator to the Counter class:

```
class Counter {
 protected:
 int count;
 public:
 Counter() { count = 0; }
 Counter(int c) { count = c; }
 int getCount() { return count; }
 Counter operator++() {
 ++count;
 return *this;
 }
 };

 class CountDn : public Counter {
 public:
 CountDn operator--() {
 --count;
 return *this;
 }
 };
```

Here's a breakdown of the syntax:

+   • The private access specifier in the Counter class has been replaced with the protected access specifier. More on this later.

+   • CountDn is the derived class name

+   • : specifies that CountDn is derived from Counter

+   • public refers to the type of inheritance which may be public, private, or protected. We'll look at this at a later time.

+   • Counter is the name of the base class