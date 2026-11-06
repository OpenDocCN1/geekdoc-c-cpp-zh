```
~~~cpp
    friend std::ostream &operator<<(std::ostream &out, Base const &obj);

  public:
    virtual ~Base() = default;
    Base *clone() const;
  private:
    virtual Base *ownClone() const = 0;
    virtual std::ostream &insert(std::ostream &os) const = 0;
};

inline std::ostream &operator<<(std::ostream &out, Base const &obj)
{
    return obj.insert(out);
}

#endif
~~~
```

Instead of using fields of a classical `union` we are now using classes that are derived from the class `Base`. For example:

+   - Objects of the class `Int` contain `int` values. Here is its interface (and implementation):

```
~~~cpp
#ifndef INCLUDED_INT_
#define INCLUDED_INT_

#include <ostream>

#include <bobcat/a2x>

#include "../base/base.h"

class Int: public Base
{
    int d_value;

  public:
    Int(char const *text);
    Int(int v);
    int value() const;                  // directly access the value
  private:
    virtual Base *ownClone() const;
    virtual std::ostream &insert(std::ostream &os) const;
};

inline Int::Int(char const *text)
:
    d_value(FBB::A2x(text))
{}

inline Int::Int(int v)
:
    d_value(v)
{}

inline Base *Int::ownClone() const
{
    return new Int(*this);
}
~~~
```