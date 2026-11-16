```
int main()
{
    try
    {
        allocate_memory();
    }
    catch(...)
    {
        cout<<"Error occurred";
    }

    return 0;
}
```

# Standard exceptions

There are various predefined exceptions which have been defined for standard cases. Even C++ Standard library provides a base class specifically designed to declare objects to be thrown as exceptions, its name is exception and is defined in the <exception> header file. This class has an additional virtual member function called what that returns a null-terminated character sequence (char *) i.e. a string which is the detail of thrown error and that can be overwritten in derived classes to contain some sort of description of the exception. The class is defined as follows:

```
class exception
{
public:
    exception() _GLIBCXX_USE_NOEXCEPT {}
    virtual ~exception() _GLIBCXX_USE_NOEXCEPT;
    /** Returns a C-style character string describing the general cause
    * of the current error. */
    virtual const char* what() const _GLIBCXX_USE_NOEXCEPT;
```