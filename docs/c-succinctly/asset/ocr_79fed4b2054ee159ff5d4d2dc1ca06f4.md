```
```cpp
class Sandwich
{
public:
    Sandwich(void);
    ~Sandwich(void);

        void AddIngredient(const wchar_t* ingredient);
        void RemoveIngredient(const wchar_t* ingredient);
        void SetBreadType(const wchar_t* breadType);
        const wchar_t * GetSandwich(void);

private:
        std::unique_ptr<SandwichImpl> m_pImpl;
};
```
```

# Sample: PimplSample\\Sandwich.cpp

```
```cpp
#include "Sandwich.h"
#include <vector>
#include <string>
#include <algorithm>

using namespace std;

// We can make any changes we want to the implementation class without
// triggering a recompile of other source files that include Sandwich.h since
// SandwichImpl is only defined in this source file. Thus, only this source
// file needs to be recompiled if we make changes to SandwichImpl.
class SandwichImpl
{
public:
        SandwichImpl();
        ~SandwichImpl();

        void AddIngredient(const wchar_t* ingredient);
        void RemoveIngredient(const wchar_t* ingredient);
        void SetBreadType(const wchar_t* breadType);

        const wchar_t* GetSandwich(void);

private:
        vector<wstring>         m_ingredients;
        wstring                 m_breadType;
        wstring                 m_description;
};

SandwichImpl::SandwichImpl()
{
}

SandwichImpl::~SandwichImpl()
{
}

void SandwichImpl::AddIngredient(const wchar_t* ingredient)
{
```
```