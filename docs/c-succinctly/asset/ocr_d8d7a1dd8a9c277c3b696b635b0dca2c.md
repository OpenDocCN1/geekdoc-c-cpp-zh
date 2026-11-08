```
```cpp
public:
    ContainStuffClass(void) :
        m_regularClass(new RegularClass()),
        m_throwClass(new ThrowClass())
    {
        wcout << L"Constructing ContainStuffClass." << endl;
    }

    ContainStuffClass(const ContainStuffClass& other) :
        m_regularClass(new RegularClass(*other.m_regularClass)),
        m_throwClass(other.m_throwClass)
    {
        wcout << L"Copy constructing ContainStuffClass." << endl;
    }

    ~ContainStuffClass(void)
    {
        wcout << L"Destroying ContainStuffClass." << endl;
    }

    const wchar_t* GetString(void) const
    {
        return L"I'm a ContainStuffClass";
    }

private:
    unique_ptr<RegularClass>        m_regularClass;
    shared_ptr<ThrowClass>          m_throwClass;
};

void TerminateHandler(void)
{
    wcout << L"Terminating due to unhandled exception." << endl;

    // If you call abort (from <cstdlib>), the program will exit
    // abnormally. It will also exit abnormally if you do not call
    // anything to cause it to exit from this method.
    abort();

    /// If you were instead to call exit(0) (also from <cstdlib>),
    /// then your program would exit though nothing had
    /// gone wrong. This is bad because something did go wrong.
    /// I present this so you know that it is possible for
    /// a program to throw an uncaught exception and still
    /// exit in a way that isn't interpreted as a crash, since
    /// you may need to find out why a program keeps abruptly
    /// exiting yet isn't crashing. This would be one such cause
    /// for that.
    ///exit(0);
}

int _pmain(int /*argc*/, wchar* /*argv*/[])
{
    // Set a custom handler for std::terminate. Note that this handler
    // won't run unless you run it from a command prompt. The debugger
    // will intercept the unhandled exception and will present you with
```
```