
# How Do I Use RAII?

RAII use is described by its name: Acquiring a dynamic resource should complete the initialization of an object. If you follow this one-resource-per-object pattern, then it is impossible to wind up with a resource leak. Either you will successfully acquire the resource, in which case the object that encapsulates it will finish construction and be subject to destruction, or the acquisition attempt will fail, in which case you did not acquire the resource; thus, there is no resource to release.

The destructor of an object that encapsulates a resource must release that resource. This, among other things, is one of the important reasons why destructors should never throw exceptions, except those they catch and handle within themselves.

If the destructor threw an uncaught exception, then, to quote Bjarne Stroustrup, “All kinds of bad things are likely to happen because the basic rules of the standard library and the language itself will be violated. Don’t do it.”

As he said, *don’t do it*. Make sure you know what exceptions, if any, everything you call in your destructors could throw so you can ensure that you handle them properly.

Now you might be thinking that if you follow this pattern, you will end up writing a ton of classes. You will occasionally write an extra class here and there, but you aren’t likely to write too many because of smart pointers. Smart pointers are objects too. Most types of dynamic resources can be put into at least one of the existing smart pointer classes. When you put a resource acquisition inside a suitable smart pointer, if the acquisition succeeds, then that smart pointer object will be fully constructed. If an exception occurs, then the smart pointer object’s destructor will be called, and the resource will be freed.

There are several important smart pointer types. Let’s have a look at them.

## `std::unique_ptr`

The unique pointer, `std::unique_ptr`, is designed to hold a pointer to a dynamically allocated object. You should use this type only when you want one pointer to the object to exist. It is a template class that takes a mandatory and an optional template argument. The mandatory argument is the type of the pointer it will hold. For instance `auto result = std::unique_ptr<int>(new int());` will create a unique pointer that contains an `int*`. The optional argument is the type of deleter. We see how to write a deleter in a coming sample. Typically, you can avoid specifying a deleter since the `default_deleter`, which is provided for you if no deleter is specified, covers almost every case you can imagine.

A class that has `std::unique_ptr` as a member variable cannot have a default copy constructor. Copy semantics are disabled for `std::unique_ptr`. If you want a copy constructor in a class that has a unique pointer, you must write it. You should also write an overload for the copy operator. Normally, you want `std::shared_ptr` in that case.

However, you might have something like an array of data. You may also want any copy of the class to create a copy of the data as it exists at that time. In that case, a unique pointer with a custom copy constructor could be the right choice.

`std::unique_ptr` is defined in the `<memory>` header file.

`std::unique_ptr` has four member functions of interest.

The `get` member function returns the stored pointer. If you need to call a function that you need to pass the contained pointer to, use `get` to retrieve a copy of the pointer.

The release member function also returns the stored pointer, but release invalidates the unique_ptr in the process by replacing the stored pointer with a null pointer. If you have a function where you want to create a dynamic object and then return it, while still maintaining exception safety, use std::unique_ptr to store the dynamically created object, and then return the result of calling release. This gives you exception safety while allowing you to return the dynamic object without destroying it with the std::unique_ptr's destructor when the control exits from the function upon returning the released pointer value at the end.

The swap member function allows two unique pointers to exchange their stored pointers, so if A is holding a pointer to X, and B is holding a pointer to Y, the result of calling A::swap(B); is that A will now hold a pointer to Y, and B will hold a pointer to X. The deleters for each will also be swapped, so if you have a custom deleter for either or both of the unique pointers, be assured that each will retain its associated deleter.

The reset member function causes the object pointed to by the stored pointer, if any, to be destroyed in most cases. If the current stored pointer is null, then nothing is destroyed. If you pass in a pointer to the object that the current stored pointer points to, then nothing is destroyed. You can choose to pass in a new pointer, nullptr, or call the function with no parameters. If you pass in a new pointer, then that new object is stored. If you pass in nullptr, then the unique pointer will store null. Calling the function with no parameters is the same as calling it with nullptr.

## std::shared_ptr

The shared pointer, std::shared_ptr, is designed to hold a pointer to a dynamically allocated object and to keep a reference count for it. It is not magic; if you create two shared pointers and pass them each a pointer to the same object, you will end up with two shared pointers—each with a reference count of 1, not 2. The first one that is destroyed will release the underlying resource, giving catastrophic results when you try to use the other one or when the other one is destroyed and tries to release the already released underlying resource.

To use the shared pointer properly, create one instance with an object pointer and then create all other shared pointers for that object from an existing, valid shared pointer for that object. This ensures a common reference count, so the resource will have a proper lifetime. Let's look at a quick sample to see the right and wrong ways to create shared_ptr objects.

**Sample: SharedPtrSample\\SharedPtrSample.cpp**

```cpp
#include <memory>
#include <iostream>
#include <ostream>
#include "../pchar.h"

using namespace std;

struct TwoInts
{
        TwoInts(void) : A(), B() { }
        TwoInts(int a, int b) : A(a), B(b) { }
        int A;
        int B;
};

wostream& operator<<(wostream& stream, TwoInts* v)
{
        stream << v->A << L" " << v->B;
        return stream;
}
```

```cpp
int _pmain(int /*argc*/, wchar* /*argv*/[])
{
    /// Bad: results in double free.
    //try
    //{
    //    TwoInts* p_i = new TwoInts(10, 20);
    //
    //    auto sp1 = shared_ptr<TwoInts>(p_i);
    //    auto sp2 = shared_ptr<TwoInts>(p_i);
    //    p_i = nullptr;
    //
    //    wcout << L"sp1 count is " << sp1.use_count() << L"," << endl <<
    //        L"sp2 count is " << sp2.use_count() << L"." << endl;
    //}
    //catch(exception& e)
    //{
    //    wcout << L"There was an exception." << endl;
    //    wcout << e.what() << endl << endl;
    //}
    //catch(...)
    //{
    //    wcout << L"There was an exception due to a double free " <<
    //        L"because we tried freeing p_i twice!" << endl;
    //}

    // This is one right way to create shared_ptrs.
    {
        auto sp1 = shared_ptr<TwoInts>(new TwoInts(10, 20));
        auto sp2 = shared_ptr<TwoInts>(sp1);

        wcout << L"sp1 count is " << sp1.use_count() << L"," << endl <<
            L"sp2 count is " << sp2.use_count() << L"," << endl;

        wcout << L"sp1 value is " << sp1 << L"," << endl <<
            L"sp2 value is " << sp2 << L"." << endl;
    }

    // This is another right way. The std::make_shared function takes the
    // type as its template argument, and then the arguments (values) to the
    // constructor you want as its parameters, and it automatically
    // constructs the object for you. This is usually more memory-
    // efficient, as the reference count can be stored with the
    // shared_ptr's pointed-to object at the time of the object's creation.
    {
        auto sp1 = make_shared<TwoInts>(10, 20);
        auto sp2 = shared_ptr<TwoInts>(sp1);

        wcout << L"sp1 count is " << sp1.use_count() << L"," << endl <<
            L"sp2 count is " << sp2.use_count() << L"," << endl;

        wcout << L"sp1 value is " << sp1 << L"," << endl <<
            L"sp2 value is " << sp2 << L"." << endl;
    }

    return 0;
}
```
