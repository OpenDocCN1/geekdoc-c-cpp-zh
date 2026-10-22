```
template<auto... Values>
class Valuelist { };

int x;
using MyValueList = Valuelist<1, 'a', true, &x>;
```