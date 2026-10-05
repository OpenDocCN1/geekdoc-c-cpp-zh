
alternatives. However, you will encounter one or another raw pointer in the following paragraphs.

The most important thing is that you do not use raw pointers that own data—that is, having requested them with new and thus being implicitly responsible for calling delete. Instead, use what the standard library offers you:

- For large amounts of data, there are containers. You no longer need to build linked structures yourself; you have a wide selection.
- Every new should only go directly into a smart pointer. Better yet, use make_shared and make_unique.
- With smart pointers, you no longer need delete delete[]. These are abolished for you.
- Do not define any of the big five operations. Let the compiler handle it. This is the rule of zero.
- There are objects that cannot be copied, such as a stream or a mutex. If your class holds such fields, the compiler does the right thing: it forbids copying. Under certain circumstances, the ability to move remain. Stick to the rule of zero here.

The C++ Core Guidelines also place great emphasis on the identification of ownership. The Guideline Support Library therein offers tools as `owner<T>` to mark an owning raw pointer. Raw pointers without `owner<T>` do not own their target and are less problematic when copying. In Chapter 30, I discuss these guidelines.

## Write Your Classes Such That You Can Apply the Rule of Zero

If you use the corresponding structures of the standard library instead of the fields with ownership problems, the compiler will generate suitable copy and move operations as well as the destructor for your class.

Then you do not define or declare *any* of the big five operations for your class.

The previous example now becomes almost trivial. Depending on the use case, simply use a vector or smart pointers.

```cpp
// https://godbolt.org/z/nbh9aozPM
#include <vector>
#include <memory> // unique_ptr, shared_ptr
struct Type1 { // automatic complete copy of the resource
    std::vector<char> data;
    Type1(int n) : data(n) {}
};
struct Type2 { // copy prohibited, move allowed
    std::unique_ptr<int[]> data;
    Type2(int n) : data(new int[n]) {}
};
struct Type3 { // copy allowed, resource is then cleanly shared
    std::shared_ptr<Type1> data;
    Type3(int n) : data(std::make_shared<Type1>(n)) {}
};
```

Listing 17.2 Instead of using a raw pointer, use a standard construct and do not define any of the big five operations.

## First: Third-party

### 17.1.4 Exceptions to the Rule of Zero

libraries in particular often contain things that leave incorrect ownership after copying—for example, GUI window and database handles. Often, developers do not consider harmful copies and do not prohibit them. Here, I recommend two techniques:

- Resort to manually prohibiting copying and moving. The destructor you write must then handle the correct removal, just like a raw pointer.
- If you feel confident with C++ and smart pointers, you can use their custom deleters to handle the wrapped resource instead of the raw one. The smart pointer then manages the correct removal, and you can dispense with the big five. In some cases, the compiler can generate usable copy and move operations.

Second: When writing a class hierarchy that includes virtual methods, you must write the destructor of the base class and mark it with virtual (see Chapter 15). The body can be empty—and it will be, if you have followed the other guidelines of the rule of zero.

```cpp
// https://godbolt.org/z/6vsganWeWh
struct Base {
    virtual ~Base(); // define the destructor, make it virtual
    virtual void other();
};

struct Derived : public Base {
    void other() override;
};

int main() {
    Base *obj = new Derived();
    /* ... more lines of code here ... */
}
```

Listing 17.3 In a hierarchy with virtual methods, you must define and mark the base class destructor as virtual.

If you don't declare the destructor, the compiler will generate one. The compiler would generate it as non-virtual, and that would be bad: If the destructor is not virtual, deleting a pointer to a derived class could call the wrong destructor, as shown in the example with the delete obj line in main(). If you omit virtual ~Base(){}, the program would be incorrect.

But wait: the preceding program does not follow the rule of zero guidelines. I used a raw Base *obj pointer as an owner. That needs to be remedied. You can do this, for example, by using shared_ptr. The good news is that if you use it, you won't have a problem with incorrect cleanup even if you forget the virtual destructor. shared_ptr has built-in mechanisms that do more than the compiler alone: when removing its ward, it always calls the correct destructor, virtual or not.

```cpp
int main() {
    shared_ptr<Base> obj{ new Derived() };
    /* ... lines of code here ... */
} // obj is correctly cleaned up
```

Listing 17.4 shared_ptr always calls the correct destructor, virtual or not.

That's one more reason not to use raw pointers as owners.

If you need a polymorphic pointer, use shared_ptr instead of raw pointers.

You will know when a pointer is polymorphic: when you create pointers within an object hierarchy where the classes have virtual methods—that is, when the type of pointer is different from the type of new.

```cpp
struct Data {
    // assignment functions
    Data& operator=(Data copy) { // by value, assignment
        copy.swap(*this);
        return *this;
    }

    void swap(Data& other) { // member function
        using std::swap;
        swap(*this, other);
    }

    friend void swap(Data& a, Data& b); // free function
};
```

The swap function is useful anyway. To work well with containers, it is best to also provide swap function.

## 17.1.5 Rule of Zero, Rule of Three, Rule of Five, Rule of Four and Half

There are many tips on which of the special functions you should implement. I will summarize the various aspects here:

- Rule of zero: First, check if it is possible not to implement any of special functions. Let the compiler generate them or declare them with = default (this documents that you have forgotten the aspect). This is applicable if your class does not need to manage resources itself.
- Rule of four and half: If your class manages resources, starting with a destructor, implement all five—but you can combine assignment and move assignment (so, four). Use self-implemented swap() (four and half).
- Rule of five: Your class manages resources, but the benefit of moving is not so relevant: write a copy constructor, assignment operator, and destructor. If the compiler wants to move, it will copy.

## 17.2 Resource Acquisition Is Initialization

RAII means that when creating an object—a resource—its initialization is also done. In C++, this happens in the constructor. It is important to always leave a valid object when exiting the constructor.

This means, in particular, that even an error must not leave an invalid object lying around. If an error occurs during the initialization of the object in the constructor, you must not leave half-created data structures lying around or still blocking resources. Resource can mean many things, such as a pointer to reserved memory, an open file, or a lock for mutual exclusion of multiple processes.

In case of an error, the constructor should be exited with an exception so that the higher levels can also release their resources, However the exception must also be carefully triggered: previously requested resources must be released beforehand (or in a separate catch with rethrow) as the current instance does not (normally) regain control after the throw.

One aspect of valid is that the associated destructor must be able to completely remove the object in any case on its own and release all still existing resources. Taken together, this very effectively implements stack-based resource management.
