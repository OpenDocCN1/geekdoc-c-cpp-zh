![](bbox=[0.19, 0.105, 0.797, 0.484])

**Figure 6.5** UML class diagram of the `TCurrencyExchanger` base class and its derived `XML_CurrencyExchanger`. `TCurrencyExchanger` aggregates objects of the `TCurrency` class, as indicated by an arrow with a diamond. Only the most important class members are shown.

# **Listing 6.2** Definition of the `XML_CurrencyExchanger` class (in *CurrencyCalc_Lib, XML_CurrencyExchanger.h*).

```
```cpp
#pragma once

#include "CurrencyExchanger.h"

#include <string>
#include <regex>

using std::wregex;

namespace CppBook
{

class XML_CurrencyExchanger : public TCurrencyExchanger
{

    private:
```
```