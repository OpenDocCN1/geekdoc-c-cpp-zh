```
```cpp
using namespace CppForCsExceptions;
using namespace std;

class ThrowClass
{
public:
    ThrowClass(void)
        : m_shouldThrow(false)
    {
        wcout << L"Constructing ThrowClass." << endl;
    }

    explicit ThrowClass(bool shouldThrow)
        : m_shouldThrow(shouldThrow)
    {
        wcout << L"Constructing ThrowClass. shouldThrow = "
              << (shouldThrow ? L"true." : L"false.") << endl;

        if (shouldThrow)
        {
            throw InvalidArgumentException<const char*>(
                "ThrowClass",
                "ThrowClass(bool shouldThrow)",
                "shouldThrow",
                "true"
            );
        }
    }

    ~ThrowClass(void)
    {
        wcout << L"Destroying ThrowClass." << endl;
    }

    const wchar_t* GetShouldThrow(void) const
    {
        return (m_shouldThrow ? L"True" : L"False");
    }

private:
    bool          m_shouldThrow;
};

class RegularClass
{
public:
    RegularClass(void)
    {
        wcout << L"Constructing RegularClass." << endl;
    }

    ~RegularClass(void)
    {
        wcout << L"Destroying RegularClass." << endl;
    }
};

class ContainStuffClass
{
```
```