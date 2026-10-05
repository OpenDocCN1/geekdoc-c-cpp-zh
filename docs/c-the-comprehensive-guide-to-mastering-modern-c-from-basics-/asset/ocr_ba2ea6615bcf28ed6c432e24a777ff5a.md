```
main.cpp
#include "part1.hpp"
#include "part2.hpp"
#include "const.hpp"
int main() { ... }
```

```
part1.cpp
#include "part1.hpp"
#include "util.hpp"
int func1() { ... };
```

```
part2.hpp
#include "util.hpp"
#include "const.hpp"
int func2();
int data[2];
```

```
part2.cpp
#include "part2.hpp"
#include "part1.hpp"
int func2() { func1();... };
int data[2] = {};
```

```
util.hpp
int calcien();
```

```
util.cpp
#include "util.hpp"
#include "const.hpp"
int calcien() { ... };
```

```
const.hpp
static const int X=1;
static const int Y=2;
static const int Z=3;
```

![](bbox=[0.148, 0.172, 0.851, 0.796])

# Figure 11.2 Divide the components of your