# Sample: ConstructorsSample\Toppings.h

```
```cpp
#pragma once
#include <string>
#include <sstream>

namespace Desserts
{
        class Toppings
        {
        public:

                enum ToppingsList : unsigned int
                {
                        None = 0x00,
                        HotFudge = 0x01,
                        RaspberrySyrup = 0x02,
                        CrushedWalnuts = 0x04,
                        WhippedCream = 0x08,
                        Cherry = 0x10
                } m_toppings;

                Toppings(void) :
                        m_toppings(None),
                        m_toppingsString()
                {
                }

                Toppings(ToppingsList toppings) :
                        m_toppings(toppings),
                        m_toppingsString()
                {
                }

                ~Toppings(void)
                {
                }

                const wchar_t* GetString(void)
                {
                        if (m_toppings == None)
                        {
                                m_toppingsString = L"None";
                                return m_toppingsString.c_str();
                        }
                        bool addSpace = false;
                        std::wstringstream wstringstream;
                        if (m_toppings & HotFudge)
                        {
                                if (addSpace)
                                {
                                        wstringstream << L" ";
                                }
                                wstringstream << L"Hot Fudge";
                                addSpace = true;
                        }
                        if (m_toppings & RaspberrySyrup)
```
```