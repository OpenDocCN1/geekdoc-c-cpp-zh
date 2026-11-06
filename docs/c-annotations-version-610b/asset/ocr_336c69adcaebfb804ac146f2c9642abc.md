# 23.9. USING ‘BISONC++’ AND ‘FLEX’

```
```cpp
inline int Int::value() const
{
    return d_value;
}

inline std::ostream &Int::insert(std::ostream &out) const
{
    return out << d_value;
}

#endif
```
```

+   - Objects of the class `Text` contain text. These objects can be used, e.g., to store the names of identifiers recognized by a lexical scanner. Here is the interface of the class `Text`:

```
```cpp
#ifndef INCLUDED_TEXT_
#define INCLUDED_TEXT_

#include <string>
#include <ostream>

#include "../base/base.h"

class Text: public Base
{
    std::string d_text;

    public:
        Text(char const *id);
        std::string const &id() const;          // directly access the name.
    private:
        virtual Base *ownClone() const;
        virtual std::ostream &insert(std::ostream &os) const;
};

inline Text::Text(char const *id)
:
    d_text(id)
{}

inline Base *Text::ownClone() const
{
    return new Text(*this);
}

inline std::string const &Text::id() const
{
    return d_text;
}

inline std::ostream &Text::insert(std::ostream &out) const
{
    return out << d_text;
}

#endif
```
```

The polymorphic `Base` can’t immediately be used as the parser’s semantic value type for various reasons: