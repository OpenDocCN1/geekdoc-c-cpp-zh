# 5.6 Booleans

Rules:

+   a. Boolean variables shall be declared as type bool.

+   b. Non-Boolean values shall be converted to Boolean value via use of relational operators (e.g., < or !=), not via casts.

Example:

```
#include <stdbool.h>
...
```

```
bool b_in_motion = (0 != speed_in_mph);
```

Reasoning: The C90 standard did not define a data type for Boolean variables and programmers have widely treated any non-zero integer value as true. The C99 language standard is backward compatible with this old style, but also introduced a new data type for Boolean variables along with new constants true and false in the stdbool.h header file.

Enforcement: These rules shall be enforced during code reviews.