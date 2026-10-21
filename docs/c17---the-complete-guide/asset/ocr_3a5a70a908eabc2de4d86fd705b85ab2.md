This feature is needed in particular if a member function of the object shall yield a shared pointer to the object:

```
class Person : public std::enable_shared_from_this<Person>
{
    ...
    std::shared_ptr<Person> sharedPtrTo() {
        return shared_from_this();
    }
};
```

Since C++17, there is an additional helper function to yield a weak pointer to the object:

```
Person* pp = new Person{...};
std::shared_ptr<Person> sp{pp};                 // sp gets ownership
...
std::weak_ptr<Person> wp{pp->weak_from_this()}; // wp observes ownership of what sp owns
```

Before C++17, you could have the same functionality with

```
weak_ptr<Person> wp{pp->shared_from_this()}
```

but weak_from_this() achieves the same effect with fewer reference count modifications.

In addition, the behavior of a specific corner case was clarified: If a raw pointer is passed to two different shared pointers (which is valid if only one of them really deletes the associated resource), then shared_from_this() and weak_from_this() share the ownership with the shared pointer created first. This means that the following is possible:

```
struct Person : public std::enable_shared_from_this<Person>
{
    ...
};
```

```
Person* p = new Person;
std::shared_ptr<Person> sp1(p);      // create a first shared pointer

{
    std::shared_ptr<Person> sp2(p,      // create a second shared pointer not sharing ownership
        [](void*) {
        });
    auto sp3{p->shared_from_this()};   // sp3 shares ownership with sp1
}

auto sp4{p->shared_from_this()};      // sp4 shares ownership with sp1
```

Before this clarification, some implementations allowed sp3 and sp4 to share ownership with the shared pointer created last, which threw std::bad_weak_ptr when initializing sp4.