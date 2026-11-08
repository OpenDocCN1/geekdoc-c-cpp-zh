
```cpp
    L", Thread id: " << this_thread::get_id() << L"\n" << endl;
    Value::ThreadLocalSomeStruct.Value = value;
    wcout << L"New value is " << Value::ThreadLocalSomeStruct.Value <<
        L", Thread id: " << this_thread::get_id() << L"\n" << endl;
}

void LocalStatic(int value)
{
        static SomeClass sc(value, L"LocalStatic sc");

        //// If you wanted to reinitialize sc every time, you would have to
        //// un-comment the following line. This, however, would defeat the
        //// purpose of having a local static. You could do something
        //// similar if you wanted to reinitialize it in certain circumstances
        //// since that would justify having a local static.
        //// sc = SomeClass(value, L"LocalStatic reinitialize");

        wcout << L"Local Static sc value: " << sc.GetValue() <<
                L"\n" << endl << endl;
}

int _pmain(int /*argc*/, _pchar* /*argv*/[])
{
        // Automatic storage; destroyed when this function ends.
        SomeClass sc1(1, L"_pmain sc1");
        wcout << L"sc1 value: " << sc1.GetValue() <<
                L"\n" << endl << endl;

        {
                // The braces here create a new block. This means that
                // sc2 only survives until the matching closing brace, since
                // it also has automatic storage.
                SomeClass sc2(2, L"_pmain sc2");
                wcout << L"sc2 value: " << sc2.GetValue() <<
                        L"\n" << endl << endl;
        }

        LocalStatic(1000);
        // Note: The local static in LocalStatic will not be reinitialized
        // with 5000. See the function definition for more info.
        LocalStatic(5000);

        // To demonstrate __declspec(thread) we change the value of this
        // thread's Value::ThreadLocalSomeStruct to 20 from its default 0.
        ChangeAndPrintValue(20);

        // We now create a new thread that automatically starts and
        // changes the value of Value::ThreadLocalSomeStruct to 40. If it
        // were shared between threads, then it would be 20 from the
        // previous call to ChangeAndPrintValue. But it's not. Instead, it
        // is the default 0 that we would expect as a result of this being
        // a new thread.
        auto thr = thread(ChangeAndPrintValue, 40);

        // Wait for the thread we just created to finish executing. Note that
        // calling join from a UI thread is a bad idea since it blocks
        // the current thread from running until the thread we are calling
        // join on completes. For WinRT programming, you want to make use
// of the PPLTasks API instead.
thr.join();

// Dynamic storage. WARNING: This is a 'naked' pointer, which is a very
// bad practice. It is here to clarify dynamic storage and to serve
// as an example. Normally, you should use either
// std::unique_ptr or std::shared_ptr to wrap any memory allocated with
// the 'new' keyword or the 'new[]' keyword.
SomeClass* p_dsc = new SomeClass(1000, L"_pmain p_dsc");

const std::size_t arrIntSize = 5;

// Dynamic storage array. THE SAME WARNING APPLIES.
int* p_arrInt = new int[arrIntSize];

// Note that there's no way to find how many elements arrInt
// has other than to manually track it. Also note that the values in
// arrInt are not initialized (i.e. it's not arrIntSize zeroes, it's
// arrIntSize arbitrary integer values).

for (int i = 0; i < arrIntSize; i++)
{
    wcout << L"i: '" << i << L"'. p_arrInt[i] = '" <<
        p_arrInt[i] << L"'." << endl;

    // Assign a value of i to this index.
    p_arrInt[i] = i;
}

wcout << endl;

//// If you wanted to zero out your dynamic array, you could do this:
//uninitialized_fill_n(p_arrInt, arrIntSize, 0);

for (int i = 0; i < arrIntSize; i++)
{
    wcout << L"i: '" << i << L"'. p_arrInt[i] = '" <<
        p_arrInt[i] << L"'." << endl;
}

// If you forgot this, you would have a memory leak.
delete p_dsc;

//// If you un-commented this, then you would have a double delete,
//// which would crash your program.
//delete p_dsc;

//// If you did this, you would have a program error, which may or may
//// not crash your program. Since dsc is not an array, it should not
//// use the array delete (i.e. delete[]), but should use the non-array
//// delete shown previously.
//delete[] p_dsc;

// You should always set a pointer to nullptr after deleting it to
// prevent any accidental use of it (since what it points to is unknown
// at this point).
p_dsc = nullptr;
// If you forgot this, you would have a memory leak. If you used
// 'delete' instead of 'delete[]' unknown bad things might happen. Some
// implementations will do ...
// knows what else.
delete[] p_arrInt;
p_arrInt = nullptr;

wcout << L"Ending program." << endl;
return 0;
}
```

For whom it is inconvenient to run the sample, here is the output I get when I run this from a command prompt on Windows 8 Release Preview, compiled with Visual Studio 2012 Ultimate RC in Debug configuration targeting the x86 chipset. You will probably produce different values for the addresses and thread IDs if you run it on your own system.

```text
Creating SomeClass instance.
StringId: s_someClass.
Address is: '0x009fade8'.
Value is '10'.
Thread id: '3660'.

Creating SomeClass instance.
StringId: g_staticSomeClass.
Address is: '0x013f8554'.
Value is '20'.
Thread id: '3660'.

Creating SomeClass instance.
StringId: _pmain sc1.
Address is: '0x007bfe98'.
Value is '1'.
Thread id: '3660'.

sc1 value: '1'.

Creating SomeClass instance.
StringId: _pmain sc2.
Address is: '0x007bfe70'.
Value is '2'.
Thread id: '3660'.

sc2 value: '2'.

Destroying SomeClass instance.
StringId: _pmain sc2.
Address is: '0x007bfe70'.
Thread id: '3660'.

Creating SomeClass instance.
StringId: LocalStatic sc.
Address is: '0x013f8578'.
Value is '1000'.
Thread id: '3660'.

Local Static sc value: '1000'.

Local Static sc value: '1000'.

Creating SomeClass instance.
StringId: ChangeAndPrintValue thread id: '3660'.
Address is: '0x007bfbf4'.
Value is '20'.
Thread id: '3660'.

Old value is 0. Thread id: '3660'.
New value is 20. Thread id: '3660'.
Destroying SomeClass instance.
StringId: ChangeAndPrintValue thread id: '3660'.
Address is: '0x007bfbf4'.
Thread id: '3660'.

Creating SomeClass instance.
StringId: ChangeAndPrintValue thread id: '5796'.
Address is: '0x0045faa8'.
Value is '40'.
Thread id: '5796'.

Old value is 0. Thread id: '5796'.
New value is 40. Thread id: '5796'.
Destroying SomeClass instance.
StringId: ChangeAndPrintValue thread id: '5796'.
Address is: '0x0045faa8'.
Thread id: '5796'.

Creating SomeClass instance.
StringId: _pmain p_dsc.
Address is: '0x009fbcc0'.
Value is '1000'.
Thread id: '3660'.

i: '0', p_arrInt[i] = '-842150451'.
i: '1', p_arrInt[i] = '-842150451'.
i: '2', p_arrInt[i] = '-842150451'.
i: '3', p_arrInt[i] = '-842150451'.
i: '4', p_arrInt[i] = '-842150451'.

i: '0', p_arrInt[i] = '0'.
i: '1', p_arrInt[i] = '1'.
i: '2', p_arrInt[i] = '2'.
i: '3', p_arrInt[i] = '3'.
i: '4', p_arrInt[i] = '4'.
Destroying SomeClass instance.
StringId: _pmain p_dsc.
Address is: '0x009fbcc0'.
Thread id: '3660'.

Ending program.
Destroying SomeClass instance.
StringId: _pmain sc1.
Address is: '0x007bfe98'.
Thread id: '3660'.

Destroying SomeClass instance.
StringId: LocalStatic sc.
Address is: '0x013f8578'.
Thread id: '3660'.

Destroying SomeClass instance.
StringId: g_staticSomeClass.
Address is: '0x013f8554'.
Thread id: '3660'.

Destroying SomeClass instance.
StringId: s_someClass.
Address is: '0x009fadc8'.
Thread id: '3660'.
```

## Chapter 5 Constructors, Destructors, and Operators

### Overview

C++ constructors are more complicated than their C# counterparts. For one thing, there are five types of constructors. Although you will rarely write all five types for any particular class or structure, you do need to know what they are, what they do, and what they look like. If not, you could find yourself facing some very confusing bugs or compiler errors.

The reason C++ constructors are more involved than C# constructors is the variety in storage duration that a C++ class can have. By default, C++ objects have value semantics while C# classes have reference semantics. Here’s an example:

```cpp
Vehicle someVehicle = vehicle;
```

Let’s assume vehicle is not null but is a valid object of type Vehicle, and that the Vehicle type is a class type as opposed to a structure or something else.

Let’s consider the previous code statement as if it were C# code. In C#, the object that vehicle refers to lives off somewhere in a heap managed by the GC. The previous code statement stores a reference to that object in the someVehicle variable, which it gets from the existing vehicle reference to the object. There is still just the one instance of that object with two references to it.

Let’s now consider the previous statement as if it were C++ code. In C++, the object that vehicle refers to is likely an automatic duration object, but it could be a static duration object or even a thread duration object. The previous code statement would by default create a copy of the vehicle object and store it in the address of the automatic duration someVehicle variable. It does this using something called a copy assignment operator, a close relative of a copy constructor.

There are now two copies where once there was one. Unless the Vehicle class has a pointer, a `std::shared_ptr`, a reference, or something of that sort as a member variable, the two copies are completely separate. Changing or even destroying one will have no effect whatsoever on the other.

Of course, if you want someVehicle to be a reference to vehicle’s object, you can change the code slightly and accomplish that. But what if you wanted someVehicle to become vehicle and for vehicle to stop existing—to be destroyed without taking its former resources with it? C++ makes this possible through something called a move constructor and a move assignment operator.

If you want to intentionally disable copy semantics (assignment and construction, collectively) or move semantics, that is possible too.

### Default Constructor

We’ll start with default constructors. A default constructor can be called with no arguments. A class can have no more than one default constructor. If you define a class and include no constructors, you produce an implicit default constructor, which the compiler creates for you. However, if you have a class member variable that is a class, structure, or union that has no default constructor, then you must define at least one constructor because the compiler cannot create an implicit default constructor.
