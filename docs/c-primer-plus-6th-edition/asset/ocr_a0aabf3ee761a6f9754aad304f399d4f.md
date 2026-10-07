# Inheritance and Dynamic Memory Allocation

is a friend to the baseDMA class. The next problem is that friends are not member
functions, you can't use the scope-resolution operator to indicate which function to use.
The solution to this problem is to use a type cast as prototype matching will select
the correct function. Thus, the code type casts the type const hasDMA & parameter to the
type const baseDMA & argument:

```
std::ostream & operator<<(std::ostream & os, const hasDMA & hs)
{
// type cast to match operator(std::ostream &, const baseDMA &)
os << (const baseDMA & hs);
os << "Style: " << hs.style << endl;
return os;
}
```

Listing 13.16 tests the baseDMA, lacksDMA, and hasDMA classes in a short program.

# Listing 13.16 usedma.cpp

```
// usedma.cpp -- inheritance, friends, and dma
// compile with dma.cpp
#include <iostream>
#include "dma.h"
int main()
{
  using std::cout;
  using std::endl;

  baseDMA shirt("Portably", 8);
lacksDMA balloon("red", "Limpo", 4);
hasDMA map("Mercator", "Buffalo Keys", 5);
  cout << "Displaying baseDMA object:\\n";
  cout << shirt << endl;
  cout << "Displaying lacksDMA object:\\n";
  cout << balloon << endl;
  cout << "Displaying hasDMA object:\\n";
  cout << map << endl;
lacksDMA balloon2(balloon);
  cout << "Result of lacksDMA copy:\\n";
  cout << balloon2 << endl;
  hasDMA map2;
  map2 = map;
  cout << "Result of hasDMA assignment:\\n";
  cout << map2 << endl;

  return 0;
}
```